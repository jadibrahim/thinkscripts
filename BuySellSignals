# Original post https://usethinkscript.com/threads/trend-painter-indicator-with-buy-sell-signals-for-thinkorswim.226/

case Standard:
    Line1 = ThermoScore;
    Line2 = ThermoScore;
}

def InvisibleLine = close * 0;
plot Line3 = InvisibleLine;
Line3.Hide();

def Buy = Line1 > 0 and Line2 < 0 and state == state.long;
def StrongBuy = Line1 > 0 and Line2 >= 0 and state == state.long;
def Sell = Line1 < 0 and Line2 > 0 and state == state.short;
def StrongSell = Line1 < 0 and Line2 <= 0 and state == state.short;

plot GU = BuySignal;
GU.SetPaintingStrategy(PaintingStrategy.BOOLEAN_ARROW_UP);
GU.SetDefaultColor(GetColor(8));
GU.SetLineWeight(2);

plot GX = SellSignal;
GX.SetPaintingStrategy(PaintingStrategy.BOOLEAN_ARROW_DOWN);
GX.SetDefaultColor(GetColor(8));
GX.SetLineWeight(2);

AssignPriceColor(if Buy then Color.DARK_GREEN else if StrongBuy then Color.GREEN else if Sell then Color.DARK_RED else if StrongSell then Color.RED else Color.BLUE);

AddLabel(yes, Concat("Current Reading is ", (if Buy then "Up Trend" else if StrongBuy then "Strong Up Trend" else if Sell then "Down Trend" else if StrongSell then "Strong Down Trend" else "Neutral")),  if Buy then Color.DARK_GREEN else if StrongBuy then Color.GREEN else if Sell then Color.DARK_RED else if StrongSell then Color.RED else Color.GRAY);

## Alerts ##
# Unblock comments below if you would like alerts
# Alert(GU, " ", Alert.Bar, Sound.Chimes);
# Alert(GX, " ", Alert.Bar, Sound.Bell);
