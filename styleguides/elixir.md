# Elixir styleguides

## Rules of thumb

Whenever you find yourself using conditionals(if, else, unless), know that you are looking at possible pattern matching usecase

__Good__

```elixir
def get_game(%{exist?: true}), do: {:ok, game}
def get_game(%{exist?: false}), do: {:error, :not_found}
```


__Bad__

```elixir
def get_game(game) do
   if game.exist? do
       {:ok, game}
   else
      {:error, :not_found}
   end
end
```

## with pipeline

While using with pipeline wrap your return values in tuples, so that you can match error clause in else individually.

eg: 

__Good__ 

```elixir
def join_game(user_id, game_id) do
  with {:user, {:ok, user}} <- {:user, Users.get(user_id)}, 
       {:game, {:ok, game}} <- {:game, Games.get(game_id)},
       {:full, false}       <- {:full, Game.is_full?(game)},
       {:started, false}    <- {:started, Game.is_started?(game)},
       {:allowed, true}     <- {:allowed, User.has_permission?(user, game)}
do
  Game.add_user(game, user)
else
  {:user, :not_found} -> {:error, "User not found"}
  {:game, :not_found} -> {:error, "Game not found"}
  {:full, true}       -> {:error, "Game is full"}
  {:started, true}    -> {:error, "Game has already started"}
  {:allowed, false}   -> {:error, "User is not allowed to join this game"}
end
```

__Bad__

```elixir
def join_game(user_id, game_id) do
  with {:ok, user} <- Users.get(user_id), 
       {:ok, game} <- Games.get(game_id),
       false       <- Game.is_full?(game),
       false       <- Game.is_started?(game),
       true        <- User.has_permission?(user, game)
do
  Game.add_user(game, user)
else
  :not_found -> {:error, "User or game not found"}
  true       -> {:error, "Game is full, or game has already started"}
  false      -> {:error, "User does not have permission"}
end
```

## Piping a case

Using case on a pipe opertaion result.

__Good__

```elixir
Ecto.Multi.new()
|> Ecto.Multi.insert(:team, team_changeset)
|> Ecto.Multi.update(:user, user_changeset)
|> Repo.transaction
|> case do
    {:ok, %{user: user, team: team}} ->
    # Yay, success!
    {:error, op, res, others} ->
    # One of the others failed!
end
```

__Bad__

```elixir
multi_result = Ecto.Multi.new()
|> Ecto.Multi.insert(:team, team_changeset)
|> Ecto.Multi.update(:user, user_changeset)
|> Repo.transaction

case multi_result do
    {:ok, %{user: user, team: team}} ->
    # Yay, success!
    {:error, op, res, others} ->
    # One of the others failed!
end
```

## Lazy evaluation with streams

Consider using lazy evaluation whenever multiple operation need to be performed on a large enumerable.

__Good__

```elixir
1..100_000 
|> Stream.map(&(&1 * 3)) 
|> Stream.filter(odd?) 
|> Enum.sum
```

__Bad__

```elixir
1..100_000 
|> Enum.map(&(&1 * 3)) 
|> Enum.filter(odd?) 
|> Enum.sum
```