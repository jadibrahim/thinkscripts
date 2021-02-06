declare upper;

input over_bought = 80;
input over_sold = 20;
input KPeriod = 10;
input DPeriod = 10;
input priceH = high;
input priceL = low;
input priceC = close;
input slowing_period = 3;
input smoothingType = {default SMA, EMA};

def lowest_k = Lowest(priceL, KPeriod);
def c1 = priceC - lowest_k;
def c2 = Highest(priceH, KPeriod) - lowest_k;
def FastK = if c2 != 0 then c1 / c2 * 100 else 0;

def FullK;
def FullD;

switch (smoothingType) {
case SMA:
    FullK = Average(FastK, slowing_period);
    FullD = Average(FullK, DPeriod);
case EMA:
    FullK = ExpAverage(FastK, slowing_period);
    FullD = ExpAverage(FullK, DPeriod);
}

def pricefilterup = if close > close[50] then 1 else 0;
def pricefilterdown = if close < close [50] then 1 else 0;

def OverBoughtAdd = if FullK < over_bought and FullK[1] >= over_bought then 1 else 0;
def OverSoldAdd = if FullK > over_sold and FullK[1] <= over_sold then 1 else 0;

def na = Double.NaN;

#Plot arrows
plot up = if StrongBuy and OverSoldAdd  and pricefilterup then low - (3 * TickSize()) else na;
plot down = if StrongSell and OverBoughtAdd and pricefilterdown then high + (3 * TickSize()) else na;
up.SetPaintingStrategy(PaintingStrategy.ARROW_UP);
down.SetPaintingStrategy(PaintingStrategy.ARROW_DOWN);
