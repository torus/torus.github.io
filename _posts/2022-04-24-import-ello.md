---
title: Ello のデータをインポート
---

これまで [Ello](https://ello.co/gwaihir) に書いていた記事をすべてここの Jekyll にインポートした。
Ello は JSON 形式でデータをエクスポートできるので良心的だ。

Ello は Markdown が使えるし広告も入らないし何も不満はなかったんだけど、どういう訳か Google でクロールされないという問題があった。
DuckDuckGo や Neeva では検索出来たけど、Google の検索でヒットしないとだれも見つけてくれないので寂しい。
また、自分のブログに限定して検索する機能もなかったので、思い切って GitHub Pages に引っ越したのでした。

そのついでに CSS も追加した。[Markdown CSS](https://markdowncss.github.io/) から Modest というのを選んだ。

さらに、Twitter で共有したときにページのタイトルが表示されるように
[Twitter Card](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/abouts-cards) も追加してみた。

![image](https://user-images.githubusercontent.com/65044/164972282-883d51cb-d1a6-49aa-bd6f-ab3112ef5890.png)

Ello のデータから Jekyll のデータに変換するのに、Gauche で下のようなコードを書いた：

```scheme
(use rfc.json)
(use util.match)
(use json-match)

(define (write-body % @ e)
  ((% "body"
      (@
       (^e
        (match (assoc "kind" e)
               ('("kind" . "text")
                (print (cdr (assoc "data" e))))
               ('("kind" . "image")
                (let ((image-url
                       (json-query e '("data" "url"))))
                  (print #"![](~|image-url|)")))
               ('("kind" . "embed")
                (match (json-query e '("data" "service"))
                       ("youtube"
                        (let ((youtube-id
                               (json-query e '("data" "id"))))
                          (print #"<iframe width=\"560\" height=\"315\" src=\"https://www.youtube.com/embed/~|youtube-id|\" title=\"YouTube video player\" frameborder=\"0\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" allowfullscreen></iframe>"))
                        ))))
        (print ""))))
   e))

(let ((json (parse-json (open-input-file "ello.json"))))
  (json-match
   json
   (^[% @]
     (% "posts"
        (@ (^e
            (let* ((id (cdr (assoc "id" e)))
                   (date-str (cdr (assoc "created_at" e)))
                   (date-match (#/(\d+-\d+-\d+)T(\d+:\d+:\d+)/ date-str))
                   (front-date #"~(date-match 1) ~(date-match 2) +0")
                   (filename #"~(date-match 1)-ello-~|id|.md"))
              (with-output-to-file #"../content/_posts/~filename"
                (^[]
                  (print #"---")
                  (print #"date: ~front-date")
                  (print #"title: Ello ~date-str")
                  (print #"---")

                  (write-body % @ e)
                  ))
              ))
           ))
     )))
```

json-match というのはお手製の JSON パターンマッチャでこんなのです：

```scheme
(define-module json-match
  (export json-match-object
          json-match-array
          json-match
          json-query))

(select-module json-match)


(define (json-match-object json key resolve reject)
  (if (pair? json)
      (let ((val (assoc key json)))
        (if val
            (resolve (cdr val))
            (reject "key not found")))
      (reject "not an object")))

(define (json-match-array json resolve reject)
  (vector-for-each (^v (resolve v)) json)
  #t)

(define (json-match json proc)
  (define (reject err)
    #?=err
    #f)

  (define (o key proc)
    (^j
     (define (resolve result)
       (proc result)
       #t)
     (json-match-object j key resolve reject)))

  (define (a . procs)
    (^j
     (define (resolve result)
       (let loop ((procs procs))
         (if (null? procs)
             #t
             (and
              ((car procs) result)
              (loop (cdr procs))))))

     (json-match-array j resolve reject)))

  ((proc o a) json)
  )

;; Utilities

(define (json-query json path)
  (let loop ((path path)
             (json json))
    (if (null? path)
        json
        (let ((p (car path)))
          (if (number? p)
              (loop (cdr path) (vector-ref json p))
              (loop (cdr path) (cdr (assoc p json))))))))
```


