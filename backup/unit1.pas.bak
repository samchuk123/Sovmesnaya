unit Unit1;

{$mode objfpc}{$H+}

interface

uses
  Classes, SysUtils, FileUtil, TAGraph, TASeries, Forms, Controls, Graphics,
  Dialogs, StdCtrls;

type

  { TForm1 }

  TForm1 = class(TForm)
    Button1: TButton;
    Button2: TButton;
    Button3: TButton;
    Chart1: TChart;
    Chart1LineSeries1: TLineSeries;
    Edit1: TEdit;
    Edit2: TEdit;
    Edit3: TEdit;
    Label1: TLabel;
    Label2: TLabel;
    Label3: TLabel;
    Label4: TLabel;
    Label5: TLabel;
    Label6: TLabel;
    Label7: TLabel;
    Memo1: TMemo;
    procedure Button1Click(Sender: TObject);
    procedure Button2Click(Sender: TObject);
    procedure Button3Click(Sender: TObject);
    procedure Newton(x1, eps: real; var x2: real; var k: integer);
    procedure Plot(x, y: real);
  private
    { private declarations }
  public
    { public declarations }
  end;

var
  Form1: TForm1;

implementation

{$R *.lfm}

{ TForm1 }

function F(x: real): real;
begin
  F := arctan(2 * x) - (1 / (1 + x));
end;

function F1(x: real): real;
begin
  F1 := (2 / (4 * sqr(x) + 1)) + (1 / sqr(x + 1));
end;

procedure TForm1.Newton(x1, eps: real; var x2: real; var k: integer);
var
  b: real;
begin
  x2 := x1;
  k := 0;
  repeat
    b := x2;
    Memo1.Lines.Add('x1 = ' + FloatToStrF(x2, FFFixed, 2, 7));
    Inc(k);
    x2 := b - F(b) / F1(b);
    Memo1.Lines.Add('x2 = x1 - ' + '(' + FloatToStrF(F(b), FFFixed, 2, 7) +
      ')' + ' / ' + '(' + FloatToStrF(F1(b), FFFixed, 2, 7) + ')');
    Memo1.Lines.Add('');
  until abs(x2 - b) < eps;
end;

procedure TForm1.Plot(x, y: real);
begin
  x := 0;
  while x <= 1 do
  begin
    x := x + 0.001;
    y := arctan(2 * x) - (1 / (1 + x));
    Chart1LineSeries1.AddXY(x, y);
  end;
end;

procedure TForm1.Button1Click(Sender: TObject);
var
  x0, x, eps, lg, pg: real;
  ib1: string;
  code, k: integer;
begin
  lg:=StrToFloat(Edit1.Text);
  pg:=StrToFloat(Edit2.Text);
  eps :=StrToFloat(Edit3.Text);
  ib1 := InputBox('Начальное приближение', 'Введите начальное приближение', '');
  val(ib1, x0, code);
  if (x0 < lg) or (x0 > pg) or (code <> 0) then
    MessageDlg('Ошибка ввода', mtError, [mbOK], 0)
  else
  begin
    Newton(x0, eps, x, k);
    Memo1.Lines.Add('x1 = ' + FloatToStrF(X, FFFixed, 2, 7));
    Label6.Caption:=('Искомый корень: ' + FloatToStrF(X, FFFixed, 2, 7));
    Memo1.Lines.Add('Количество итераций: ' + IntToStr(k));
    Plot(0,1);
    Chart1LineSeries1.AddXY(x, x0);
    Chart1Lineseries1.AddXY(x,0);
  end;

end;


procedure TForm1.Button2Click(Sender: TObject);
  const n = 5;
var
  a, b, e, pred, x, s: real;
  i: integer;

  function fh(x: real): real;
  begin
   fh := arctan(2 * x) - (1 / (1 + x));
  end;

begin
  a := strtofloat(edit1.Text);
  b := strtofloat(edit2.Text);
  e := strtofloat(edit3.Text);
  pred := b;
  x := a;
  repeat
    s := x;
    x := x - (fh(x) * (x - pred)) / (fh(x) - fh(pred));
    pred := s;
    memo1.Lines.Add(floatToStrF(x, FFFixed, 6, 7));
    for i := 1 to n do
      Chart1LineSeries1.AddXY(pred + (x - pred) * i / 5, fh(pred + (x - pred) * i / 5));
  until (abs(x - pred) < e);
  if (x >= a) and (x <= b) then
    label7.Caption := ('Искомый корень: ' + floatToStrF(x, FFFixed, 6, 7))
  else
    label7.Caption := ('На промежутке корней не найдено');

end;

procedure TForm1.Button3Click(Sender: TObject);
begin
  Memo1.Lines.Clear;
  Chart1LineSeries1.Clear;
  Label6.Caption := '';
  Label7.Caption := '';
  Edit1.Text := '';
  Edit2.Text := '';
  Edit3.Text :='';
end;

end.

