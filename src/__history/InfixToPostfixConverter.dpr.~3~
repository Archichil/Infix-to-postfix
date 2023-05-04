program InfixToPostfixConverter;

{$APPTYPE CONSOLE}

uses
  System.SysUtils,
  System.Generics.Collections;

var
  ExpressionRank: integer;
  Expression: string;

Procedure InputExpression(var AExpression: string);
begin
  write('Input an expression to convert it from infix form to postfix form (reversed polish notation) and count its rank: ');
  readln(AExpression);
end;

Function GetPrecedence(ASymbol: char): integer;
begin
  case ASymbol of
    'A'..'Z', 'a'..'z', '0'..'9': Result := 7;
    '+', '-': Result := 1;
    '*', '/': Result := 3;
    '^': Result := 6;
    '(': Result := 9;
    ')': Result := 0;
  else
    Result := -1;
  end;
end;

Function GetStackPrecedence(ASymbol: char): integer;
begin
  case ASymbol of
    'A'..'Z', 'a'..'z', '0'..'9': Result := 8;
    '+', '-': Result := 2;
    '*', '/': Result := 4;
    '^': Result := 5;
    '(': Result := 0;
  else
    Result := -1;
  end;

end;

Function GetSymbolRank(ASymbol: char): integer;
begin
  case ASymbol of
    '+', '-', '*', '/', '^': Result := -1;
    'A'..'Z', 'a'..'z': Result := 1;
  else
    Result := 0;
  end;
end;

Function InfixToPostfix(var AExpressionRank: integer; AExpression: string): string;
var
  Stack: TStack<Char>;
  Queue: string;
  i: integer;
begin
  Queue:= '';
  Stack:= TStack<Char>.Create;
  AExpressionRank:= 0;

  for I := 1 to length(AExpression) do
  begin

    // If the character is an operand, add it to output.
    if GetPrecedence(AExpression[i]) = 7 then
    begin
  		Queue := Queue + AExpression[i];
      AExpressionRank := AExpressionRank + GetSymbolRank(AExpression[i]);
    end
    else

      // If the scanned character is an open bracket, push it to the stack.
      if GetPrecedence(AExpression[i]) = 9 then
        Stack.Push(AExpression[i])
    else

      // If the scanned character is an
      // close bracket, pop and add to output from the stack
      // until an open bracket is encountered.
      if GetPrecedence(AExpression[i]) = 0 then
      begin
        while (Stack.Count <> 0) and (GetStackPrecedence(Stack.Peek) <> 0) do
        begin
          Queue := Queue + Stack.Peek;
          AExpressionRank := AExpressionRank + GetSymbolRank(Stack.Peek);
          Stack.Pop;
        end;

        // Remove open bracket from the stack
        Stack.Pop;
      end
    else
      begin
        while ((Stack.Count <> 0) and (GetPrecedence(AExpression[i]) <= GetStackPrecedence(Stack.Peek))) do
        begin
          AExpressionRank := AExpressionRank + GetSymbolRank(Stack.Peek);
          Queue := Queue + Stack.Peek;
          Stack.Pop;
        end;
      Stack.Push(AExpression[i]);
      end;

  end;

  while not (Stack.Count = 0) do
  begin
    AExpressionRank := AExpressionRank + GetSymbolRank(Stack.Peek);
    Queue := Queue + Stack.Peek;
    Stack.Pop;
  end;

  Stack.Destroy;
  Result := Queue;
end;

Procedure Output(AAExpression: string; var AAExpressionRank: integer);
begin
  writeln('Postfix form: ' ,InfixToPostfix(AAExpressionRank, AAExpression));
  writeln('Expression rank: ', AAExpressionRank);
  if AAExpressionRank = 1 then
    writeln('Expression is accurate.')
  else
    writeln('Expression is inaccurate.')
end;


begin
  InputExpression(Expression);
  Output(Expression, ExpressionRank);
  readln;
end.
