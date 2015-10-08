# Ruby Study

## メソッドについて

### インスタンスメソッド

- 何かしらのクラスのインスタンスから呼び出すメソッド

```ruby
class Foo
  def bar
    :hoge
  end
end

foo = Foo.new
foo.bar
=> :hoge
```

### クラスメソッド

- クラスから呼び出すメソッド

```ruby
class Foo
  def self.bar
    :hoge
  end
end

Foo.bar
=> :hoge
```

### 関数的メソッド

- レシーバを省略して呼ばれるメソッド

```ruby
puts 'a'
a
=> nil

print 'a'
a=> nil

p 'a'
"a"
=> "a"
```

#### privateメソッド

- クラス内でprivateで定義したメソッド
- これも関数的メソッドになる

```ruby
class Foo
  def bar
    hoge
  end

  private
    def hoge
      :hoge
    end
end

foo = Foo.new
foo.bar
=> :hoge
```

#### ちなみに

- 先ほどの`puts`、`print`、`p`は`Object`クラスのprivateメソッドにあたる


## 特異クラス・特異メソッドについて

- 特定のオブジェクトにしか存在しないクラス
- そのクラスにあるメソッドを`特異メソッド`と呼びます
- 逆に特異クラスは特異メソッドのために存在するクラス
- 奥深いので詳細は本など読んでください

### 特異クラス

- コードで説明すると。。。

```ruby
class Foo
end

Foo.superclass
=> Object

foo = Foo.new
=> #<Foo:0x007fd4291898b8>
foo.class
=> Foo
foo.class.superclass
=> Object

foo.singleton_class
=> #<Class:#<Foo:0x007fd4291898b8>>
foo.singleton_class.superclass
=> Foo
foo.singleton_class.superclass.superclass
=> Object
```

### 特異メソッド

- 特異クラス内で定義されているメソッド
- 定義方法は以下のような方法がある

#### 定義方法１

```ruby
class Foo
end

def Foo.bar
  :HOGE
end

Foo.bar
=> :HOGE

foo = Foo.new

def foo.bar
  :hoge
end

foo.bar
=> :hoge
```

#### 定義方法２

```ruby
class Foo
end

class << Foo
  def bar
    :HOGE
  end
end

Foo.bar
=> :HOGE

foo = Foo.new

class << foo
  def bar
    :hoge
  end
end

foo.bar
=> :hoge
```
