# Advent of Code Elixir Starter

A batteries included starter pack for participating in [Advent of Code](https://www.adventofcode.com) using Elixir and GitPod! The vast majority of this is from [mhanberg's Advent of Code Elixir Starter](https://github.com/mhanberg/advent-of-code-elixir-starter).

Basically, there are only a few things I've done differently:

1) I added GitPod YAML and Dockerfiles to automatically install the dependencies you'll need.
2) I got sick of remaking the secrets.exs file, so I removed it from the .gitignore and decided to put my Cookie string in GitPod's environment variables.

As a newbie to both Elixir and GitPod, I decided to write down the steps I took in case someone else might find them useful. :)

## Usage

There are 25 modules, 25 tests, and 50 mix tasks.

1. Fill in the tests with the example solutions.
1. Write your implementation.
1. Fill in the final problem inputs into the mix task and run `mix d01.p1`!
    - Benchmark your solution by passing the `-b` flag, `mix d01.p1 -b`
    - Test by running `mix test`

```elixir
defmodule AdventOfCode.Day01 do
  def part1(args) do
  end

  def part2(args) do
  end
end
```

```elixir
defmodule AdventOfCode.Day01Test do
  use ExUnit.Case

  import AdventOfCode.Day01

  @tag :skip # Make sure to remove to run your test.
  test "part1" do
    input = nil
    result = part1(input)

    assert result
  end

  @tag :skip # Make sure to remove to run your test.
  test "part2" do
    input = nil
    result = part2(input)

    assert result
  end
end
```

```elixir
defmodule Mix.Tasks.D01.P1 do
  use Mix.Task

  import AdventOfCode.Day01

  @shortdoc "Day 01 Part 1"
  def run(args) do
    input = AdventOfCode.Input.get!(1, 2020)

    if Enum.member?(args, "-b"),
      do: Benchee.run(%{part_1: fn -> input |> part1() end}),
      else:
        input
        |> part1()
        |> IO.inspect(label: "Part 1 Results")
  end
end
```

### Optional Automatic Input Retriever

This starter comes with a module that will automatically get your inputs so you don't have to mess with copy/pasting. Don't worry, it automatically caches your inputs to your machine so you don't have to worry about slamming the Advent of Code server. You will need to configure it with your cookie and make sure to enable it. You can do this by setting a persistent environment variable in your GitPod environment and updating the current session with the following commands:

```bash
gp env AOC_COOKIE="..."
eval $(gp env -e)
```

Replace the "..." with your Advent of Code session cookie, which you can find by visiting the Advent of Code website, going to any one of the input pages, and examining the input.txt file in the Network tab of your browser's inspector.

You can now retrieve your inputs using the module!

```elixir
day = 1
year = 2020
AdventOfCode.Input.get!(day, year)
# or just have it auto-detect the current year
AdventOfCode.Input.get!(7)
# and if your input somehow gets mangled and you need a fresh one:
AdventOfCode.Input.delete!(7, 2019)
# and the next time you `get!` it will download a fresh one -- use this sparingly!
```