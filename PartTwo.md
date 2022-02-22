The Second Lesson
=================

## Control Structures

### if
### unless
### case
### cond
### with


## Recursion
## Maps
## Structs
## Enum module
## Stream module

## Processes

### spawn

```
defmodule SimpleProc do
  def start(name) do
    spawn(fn -> loop(name) end)
  end

  def stop(pid) do
    Process.exit(pid, :kill)
  end

  defp loop(name) do
    IO.puts "Hello #{name}"
    Process.sleep(5_000)
    loop(name)
  end
end
```

### send/recieve

```
defmodule ReplyProcess do
  def start(name) do
    spawn(fn ->
      loop(name)
    end)
  end

  def get_answer(pid) do
    send(pid, {:name, self()})
    receive do
      {:reply, name} -> IO.puts("Response from #{name}")
    end
  end

  def stop(pid) do
    Process.exit(pid, :kill)
  end

  defp loop(name) do
    receive do
      {:name, pid} ->
        send(pid, {:reply, name})
      after 5_000 ->
        IO.puts "#{name} is waiting"
    end
    loop(name)
  end
end
```
### Agent

```
pid = Agent.start(fn -> 42 end)

```

### Task
### GenServer
### Supervisor
