---
title: Emacs の Lua mode の設定
---

Lua の BDD のテストコードを書くとインデントが深くなりがちなので、それを抑えるための設定を探してみた。
Customize Group で Lua の設定を開いて、Lua Indent Level と Lua Indent Nested Block Content Align を下のように変更した。

```lisp
 '(lua-indent-level 2)
 '(lua-indent-nested-block-content-align nil)
```

テストコードでは関数の引数に関数を渡すので、lua-indent-nested-block-content-align を使うとその部分のインデントが控えめになる。

#### 使用前
```lua
describe("state", function()
           describe("new", function()
                      it("should create a new state", function()
                           local s = State:new()
                           assert.equals(getmetatable(s), State)
                           assert.same(s, {hello = ""})
                      end)
           end)
           describe("hello", function()
                      it("should hello", function()
                           local s = State:new()
                           local result = s:hello()
                           assert.equals(result, "hello")
                      end)
           end)
end)
```

#### 使用後

```lua
describe("state", function()
    describe("new", function()
        it("should create a new state", function()
            local s = State:new()
            assert.equals(getmetatable(s), State)
            assert.same(s, {hello = ""})
        end)
    end)
    describe("hello", function()
        it("should hello", function()
             local s = State:new()
             local result = s:hello()
             assert.equals(result, "hello")
        end)
    end)
end)
```
