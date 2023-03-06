# X-and-O

program TicTacToe;

uses crt;

type
  BoardType = array[1..3, 1..3] of char;

var
  board: BoardType;
  player: char;
  row, col: integer;

procedure InitializeBoard(var board: BoardType);
var
  i, j: integer;
begin
  for i := 1 to 3 do
    for j := 1 to 3 do
      board[i,j] := ' ';
end;

procedure DisplayBoard(board: BoardType);
begin
  clrscr;
  writeln('     1   2   3');
  writeln('   +---+---+---+');
  writeln(' 1 | ', board[1,1], ' | ', board[1,2], ' | ', board[1,3], ' |');
  writeln('   +---+---+---+');
  writeln(' 2 | ', board[2,1], ' | ', board[2,2], ' | ', board[2,3], ' |');
  writeln('   +---+---+---+');
  writeln(' 3 | ', board[3,1], ' | ', board[3,2], ' | ', board[3,3], ' |');
  writeln('   +---+---+---+');
end;

function GetPlayerInput(player: char; var row, col: integer): boolean;
var
  input: string;
begin
  repeat
    write('Player ', player, ', please enter your move (row,column): ');
    readln(input);
    val(copy(input, 1, 1), row);
    val(copy(input, 3, 1), col);
  until (row >= 1) and (row <= 3) and (col >= 1) and (col <= 3) and (board[row,col] = ' ');
  GetPlayerInput := true;
end;

function CheckForWin(board: BoardType; player: char): boolean;
var
  i: integer;
begin
  CheckForWin := false;
  for i := 1 to 3 do
  begin
    if (board[i,1] = player) and (board[i,2] = player) and (board[i,3] = player) then
    begin
      CheckForWin := true;
      exit;
    end;
    if (board[1,i] = player) and (board[2,i] = player) and (board[3,i] = player) then
    begin
      CheckForWin := true;
      exit;
    end;
  end;
  if (board[1,1] = player) and (board[2,2] = player) and (board[3,3] = player) then
  begin
    CheckForWin := true;
    exit;
  end;
  if (board[1,3] = player) and (board[2,2] = player) and (board[3,1] = player) then
  begin
    CheckForWin := true;
    exit;
  end;
end;

procedure PlayGame();
var
  winner: char;
  turn: integer;
begin
  InitializeBoard(board);
  DisplayBoard(board);
  player := 'X';
  for turn := 1 to 9 do
  begin
    if GetPlayerInput(player, row, col) then
    begin
       board[row,col] := player;
  DisplayBoard(board);
  if CheckForWin(board, player) then
  begin
    winner := player;
    break;
  end;
  if player = 'X' then
    player := 'O'
  else
    player := 'X';
end;
end;
if winner <> '' then
writeln('Player ', winner, ' wins!')
else
writeln('It''s a tie!');
end;

begin
PlayGame();
readln;
end.
