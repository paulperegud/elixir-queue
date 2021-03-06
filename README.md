# Qex [![Hex.pm](https://img.shields.io/hexpm/v/qex.svg)](https://hex.pm/packages/qex) [![Documentation](https://img.shields.io/badge/docs-hexpm-blue.svg)](https://hexdocs.pm/qex/Qex.html)

A `:queue` wrapper with improvements in API and addition of Protocol implementations

### Protocols

`Inspect`, `Collectable` and `Enumerable` are implemented,
use Qex with `IO.inspect` and `Enum` functions!

### Function signatures

Parameters are re-ordered to better suit Elixir's awesome `|>`

## Installation

The package can be installed as:

  1. Add `qex` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [{:qex, "~> 0.3"}]
end
```

  2. Run `mix deps.get`

## How to use

[Read the docs](https://hexdocs.pm/qex/Qex.html)

#### Protocols

    iex> inspect Qex.new
    "#Qex<[]>"

    iex> Enum.count Qex.new(1..5)
    5

    iex> Enum.empty? Qex.new
    true

    iex> Enum.map Qex.new([1, 2, 3]), &(&1 + 1)
    [2, 3, 4]

    iex> inspect Enum.into(1..5, %Qex{})
    "#Qex<[1, 2, 3, 4, 5]>"

#### Create a new queue from a range

    iex> inspect Qex.new(1..3)
    "#Qex<[1, 2, 3]>"

#### Create a new queue from a list

    iex> inspect Qex.new([1, 2, 3])
    "#Qex<[1, 2, 3]>"

#### Add an element to the back of the queue

    iex> q = Qex.new([:mid])
    iex> Enum.to_list Qex.push(q, :back)
    [:mid, :back]

#### Add an element to the front of the queue

    iex> q = Qex.new([:mid])
    iex> Enum.to_list Qex.push_front(q, :front)
    [:front, :mid]

#### Get and remove an element from the front of the queue

    iex> q = Qex.new([:front, :mid])
    iex> {{:value, item}, _q} = Qex.pop(q)
    iex> item
    :front

    iex> q = Qex.new
    iex> {empty, _q} = Qex.pop(q)
    iex> empty
    :empty

#### Get and remove an element from the back of the queue

    iex> q = Qex.new([:mid, :back])
    iex> {{:value, item}, _q} = Qex.pop_back(q)
    iex> item
    :back

    iex> q = Qex.new
    iex> {empty, _q} = Qex.pop_back(q)
    iex> empty
    :empty

#### Reverse a queue

    iex> q = Qex.new(1..3)
    iex> Enum.to_list q
    [1, 2, 3]
    iex> Enum.to_list Qex.reverse(q)
    [3, 2, 1]

#### Split a queue into two, the front n items are put in the first queue

    iex> q = Qex.new 1..5
    iex> {q1, q2} = Qex.split(q, 3)
    iex> Enum.to_list q1
    [1, 2, 3]
    iex> Enum.to_list q2
    [4, 5]


#### Join two queues together

    iex> q1 = Qex.new 1..3
    iex> q2 = Qex.new 4..5
    iex> Enum.to_list Qex.join(q1, q2)
    [1, 2, 3, 4, 5]



## Why not "Queue"?

The name is taken... [Hex link](https://hex.pm/packages/queue)
