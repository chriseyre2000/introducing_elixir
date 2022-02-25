The Second Lesson
=================

## Control Structures

### if
### unless
### case
### cond
### with
```
defp find_person(1), do: {:ok, 21}
defp find_person(_), do: {:error, :bad_person}

defp find_address(21), do: {:ok, :the_address}
defp find_address(_), do: {:error, :no_address}

def combined(id) do
  with {:ok, person} = find_person(id),
       {:ok, address} = find_address(person)
  do
    address
  end
end
```

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
