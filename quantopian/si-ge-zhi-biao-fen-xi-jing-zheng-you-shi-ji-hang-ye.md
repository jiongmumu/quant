# 四个指标分析竞争优势及行业



```python
# First, we need to import Fundamentals in any notebook that uses them
from quantopian.pipeline import Pipeline
from quantopian.research import run_pipeline
from quantopian.pipeline.data import Fundamentals
from quantopian.pipeline.experimental import QTradableStocksUS

# Import the StaticAsset filter since we already know the specific stocks we want data for
from quantopian.pipeline.filters import StaticAssets
```

```python
# We're going to need a date string for some of our queries. Let's grab one.
import datetime

today = datetime.datetime.now().strftime('%Y-%m-%d')
today
```

```text
'2019-01-08'
```

```python
#Fundamentals.net_income_cash_flow_statement?
#Pipeline?
```

```python
# Create pipeline filters on the market cap and p/e ratio
big_market_cap = Fundamentals.market_cap.latest > 1e9
big_pe = Fundamentals.pe_ratio.latest > 5 
small_pe = Fundamentals.pe_ratio.latest < 30

# Combine those pipeline filters with the QTradableStocksUS, a liquid trading universe
# https://www.quantopian.com/posts/working-on-our-best-universe-yet-qtradablestocksus
universe = QTradableStocksUS() & big_market_cap & big_pe & small_pe

# Define which stocks you want to get data for
my_stocks = StaticAssets(symbols([
                        'HRB',#布洛克税务公司
                        'KHC',#卡夫亨氏
                        'KO',#可口可乐
                        'DIS',#迪士尼
                        'ADBE',#Adbobe
                        'MTCH',#okcupid等
                        'AMZN',
                        'JD',
                        'NTES',#网易
                        'BABA',#阿里巴巴
                        'INTC',#英特尔
                        'TCEHY',#腾讯控股
                        'AAPL'])
                        )

# Create the pipeline
pipe = pipe = Pipeline(
    columns = {
        'pe_ratio' : Fundamentals.pe_ratio.latest,
        'morningstar_industry_code':Fundamentals.morningstar_industry_code.latest,
        'morningstar_industry_group_code': Fundamentals.morningstar_industry_group_code.latest,
        'market_cap' : Fundamentals.market_cap.latest,
        #'net_income_from_continuing_operations' : Fundamentals.net_income_from_continuing_operations.latest,
        #'cash_flow_from_continuing_financing_activities' : Fundamentals.cash_flow_from_continuing_financing_activities.latest,
        #'net_income_growth' : Fundamentals.net_income_growth.latest,
        'capital_expenditure' : Fundamentals.capital_expenditure.latest,
        'operating_revenue' : Fundamentals.operating_revenue.latest,
        'revenue_growth' : Fundamentals.revenue_growth.latest,
        'normalized_net_profit_margin' : Fundamentals.normalized_net_profit_margin.latest,
        'roe' : Fundamentals.roe.latest,
        'roa' : Fundamentals.roa.latest,
    },
    screen = my_stocks
)

# Run the pipeline
# P97 find earnings managerment companies.
fundamental_data = run_pipeline(pipe, start_date = today, end_date = today)
```

```python
fundamental_data.sort_values('roe')
```

|  |  | capital\_expenditure | market\_cap | morningstar\_industry\_code | morningstar\_industry\_group\_code | normalized\_net\_profit\_margin | operating\_revenue | pe\_ratio | revenue\_growth | roa | roe |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2019-01-08 00:00:00+00:00 | Equity\(3660 \[HRB\]\) | -5.436500e+07 | 5.199854e+09 | 10214030 | 10214 | -1.147507 | 1.488710e+08 | 9.166667 | 0.056917 | -0.072866 | -2.194070 |
| Equity\(49229 \[KHC\]\) | -1.560000e+08 | 5.527698e+10 | 20531077 | 20531 | 0.098777 | 6.378000e+09 | 5.364497 | 0.015605 | 0.005215 | 0.009614 |  |
| Equity\(21669 \[NTES\]\) | NaN | 3.145191e+10 | 31168144 | 31168 | 0.092885 | NaN | 28.866910 | 0.350824 | 0.020546 | 0.036702 |  |
| Equity\(2190 \[DIS\]\) | -1.201000e+09 | 1.645875e+11 | 10210023 | 10210 | 0.125344 | 1.430700e+10 | 13.224880 | 0.119571 | 0.023527 | 0.048956 |  |
| Equity\(46979 \[JD\]\) | NaN | 3.247163e+10 | 10217037 | 10217 | 0.028799 | NaN | 162.887891 | 0.251020 | 0.013886 | 0.049106 |  |
| Equity\(47740 \[BABA\]\) | NaN | 3.680432e+11 | 10217037 | 10217 | 0.236447 | NaN | 42.727825 | 0.544719 | 0.024710 | 0.049182 |  |
| Equity\(114 \[ADBE\]\) | -6.355800e+07 | 1.119095e+11 | 31165133 | 31165 | 0.298177 | 2.291076e+09 | 47.367769 | 0.244424 | 0.043607 | 0.075855 |  |
| Equity\(16841 \[AMZN\]\) | -3.352000e+09 | 7.967793e+11 | 10217037 | 10217 | 0.052453 | 5.657600e+10 | 91.237962 | 0.293343 | 0.020756 | 0.077793 |  |
| Equity\(3951 \[INTC\]\) | -3.851000e+09 | 2.165162e+11 | 31169147 | 31169 | 0.334013 | 1.916300e+10 | 14.732919 | 0.186637 | 0.050336 | 0.090412 |  |
| Equity\(4283 \[KO\]\) | -3.050000e+08 | 1.998433e+11 | 20530073 | 20530 | 0.288781 | 8.245000e+09 | 64.315068 | -0.091760 | 0.021307 | 0.102769 |  |
| Equity\(24 \[AAPL\]\) | -3.041000e+09 | 7.019867e+11 | 31167138 | 31167 | 0.224563 | 6.290000e+10 | 12.420655 | 0.196295 | 0.039515 | 0.127197 |  |
| Equity\(49608 \[MTCH\]\) | -6.495000e+06 | 1.206060e+10 | 31168144 | 31168 | 0.294040 | 4.439430e+08 | 36.141667 | 0.292719 | 0.057326 | 0.216641 |  |

## [morning star industry code](https://www.quantopian.com/posts/morningstar-industry-code)



```text
from quantopian.pipeline.data import morningstar as ms 

sphere = ms.asset_classification.morningstar_economy_sphere_code.latest  
industry_code = ms.asset_classification.morningstar_industry_code.latest  
industry_group = ms.asset_classification.morningstar_industry_group_code.latest  
sector = ms.asset_classification.morningstar_sector_code.latest
```

Sector is used quite often so there is a convenience method that can be used.

```text
from quantopian.pipeline.classifiers.morningstar import Sector

sector =  Sector(mask=universe)
```

The sector codes can be found in the appendix \(link is above\). Here is a convenient list to cut and paste if needed.

```text
MORNINGSTAR_SECTOR_CODES = {  
     -1: 'Misc',  
    101: 'Basic Materials',  
    102: 'Consumer Cyclical',  
    103: 'Financial Services',  
    104: 'Real Estate',  
    205: 'Consumer Defensive',  
    206: 'Healthcare',  
    207: 'Utilities',  
    308: 'Communication Services',  
    309: 'Energy',  
    310: 'Industrials',  
    311: 'Technology' ,  
}
```



```text
MORNINGSTAR_INDUSTRY_CODES = {  
  10101001: "Agricultural Inputs",  
  10102002: "Building Materials",  
  10103003: "Chemicals",  
  10103004: "Specialty Chemicals",  
  10104005: "Coal",  
  10105006: "Lumber & Wood Production",  
  10105007: "Paper & Paper Products",  
  10106008: "Aluminum",  
  10106009: "Copper",  
  10106010: "Gold",  
  10106011: "Industrial Metals & Minerals",  
  10106012: "Silver",  
  10107013: "Steel",  
  10208014: "Advertising Agencies",  
  10208015: "Marketing Services",  
  10209016: "Auto & Truck Dealerships",  
  10209017: "Auto Manufacturers",  
  10209018: "Auto Parts",  
  10209019: "Recreational Vehicles",  
  10209020: "Rubber & Plastics",  
  10210021: "Broadcasting - Radio",  
  10210022: "Broadcasting - TV",  
  10210023: "Media - Diversified",  
  10211024: "Residential Construction",  
  10211025: "Textile Manufacturing",  
  10212026: "Apparel Manufacturing",  
  10212027: "Footwear & Accessories",  
  10212028: "Home Furnishings & Fixtures",  
  10213029: "Packaging & Containers",  
  10214030: "Personal Services",  
  10215031: "Publishing",  
  10216032: "Restaurants",  
  10217033: "Apparel Stores",  
  10217034: "Department Stores",  
  10217035: "Home Improvement Stores",  
  10217036: "Luxury Goods",  
  10217037: "Specialty Retail",  
  10218038: "Gambling",  
  10218039: "Leisure",  
  10218040: "Lodging",  
  10218041: "Resorts & Casinos",  
  10319042: "Asset Management",  
  10320043: "Banks - Global",  
  10320044: "Banks - Regional - Africa",  
  10320045: "Banks - Regional - Asia",  
  10320046: "Banks - Regional - Australia",  
  10320047: "Banks - Regional - Canada",  
  10320048: "Banks - Regional - Europe",  
  10320049: "Banks - Regional - Latin America",  
  10320050: "Banks - Regional - US",  
  10320051: "Savings & Cooperative Banks",  
  10320052: "Specialty Finance",  
  10321053: "Capital Markets",  
  10321054: "Financial Exchanges",  
  10321055: "Insurance Brokers",  
  10322056: "Credit Services",  
  10323057: "Insurance - Diversified",  
  10324058: "Insurance - Life",  
  10325059: "Insurance - Property & Casualty",  
  10326060: "Insurance - Reinsurance",  
  10326061: "Insurance - Specialty",  
  10427062: "Real Estate - General",  
  10427063: "Real Estate Services",  
  10428064: "REIT - Diversified",  
  10428065: "REIT - Healthcare Facilities",  
  10428066: "REIT - Hotel & Motel",  
  10428067: "REIT - Industrial",  
  10428068: "REIT - Office",  
  10428069: "REIT - Residential",  
  10428070: "REIT - Retail",  
  20529071: "Beverages - Brewers",  
  20529072: "Beverages - Wineries & Distilleries",  
  20530073: "Beverages - Soft Drinks",  
  20531074: "Confectioners",  
  20531075: "Farm Products",  
  20531076: "Household & Personal Products",  
  20531077: "Packaged Foods",  
  20532078: "Education & Training Services",  
  20533079: "Discount Stores",  
  20533080: "Pharmaceutical Retailers",  
  20533081: "Food Distribution",  
  20533082: "Grocery Stores",  
  20534083: "Tobacco",  
  20635084: "Biotechnology",  
  20636085: "Drug Manufacturers - Major",  
  20636086: "Drug Manufacturers - Specialty & Generic",  
  20637087: "Health Care Plans",  
  20638088: "Long-Term Care Facilities",  
  20638089: "Medical Care",  
  20639090: "Medical Devices",  
  20640091: "Diagnostics & Research",  
  20641092: "Medical Distribution",  
  20642093: "Medical Instruments & Supplies",  
  20743094: "Utilities - Independent Power Producers",  
  20744095: "Utilities - Diversified",  
  20744096: "Utilities - Regulated Electric",  
  20744097: "Utilities - Regulated Gas",  
  20744098: "Utilities - Regulated Water",  
  30845099: "Pay TV",  
  30845100: "Telecom Services",  
  30946101: "Oil & Gas Drilling",  
  30947102: "Oil & Gas E&P",  
  30948103: "Oil & Gas Integrated",  
  30949104: "Oil & Gas Midstream",  
  30950105: "Oil & Gas Refining & Marketing",  
  30951106: "Oil & Gas Equipment & Services",  
  31052107: "Aerospace & Defense",  
  31053108: "Airlines",  
  31054109: "Business Services",  
  31055110: "Conglomerates",  
  31056111: "Rental & Leasing Services",  
  31056112: "Security & Protection Services",  
  31057113: "Staffing & Outsourcing Services",  
  31058114: "Engineering & Construction",  
  31058115: "Infrastructure Operations",  
  31059116: "Farm & Construction Equipment",  
  31060117: "Industrial Distribution",  
  31061118: "Business Equipment",  
  31061119: "Diversified Industrials",  
  31061120: "Metal Fabrication",  
  31061121: "Pollution & Treatment Controls",  
  31061122: "Tools & Accessories",  
  31062123: "Airports & Air Services",  
  31062124: "Integrated Shipping & Logistics",  
  31062125: "Railroads",  
  31062126: "Shipping & Ports",  
  31062127: "Trucking",  
  31063128: "Truck Manufacturing",  
  31064129: "Waste Management",  
  31165130: "Electronic Gaming & Multimedia",  
  31165131: "Health Information Services",  
  31165132: "Information Technology Services",  
  31165133: "Software - Application",  
  31165134: "Software - Infrastructure",  
  31166135: "Communication Equipment",  
  31167136: "Computer Distribution",  
  31167137: "Computer Systems",  
  31167138: "Consumer Electronics",  
  31167139: "Contract Manufacturers",  
  31167140: "Data Storage",  
  31167141: "Electronic Components",  
  31167142: "Electronics Distribution",  
  31167143: "Scientific & Technical Instruments",  
  31168144: "Internet Content & Information",  
  31169145: "Semiconductor Equipment & Materials",  
  31169146: "Semiconductor Memory",  
  31169147: "Semiconductors",  
  31169148: "Solar"  
}
```



```text
MORNINGSTAR_INDUSTRY_GROUP_CODES = {  
  10101: "Agriculture",  
  10102: "Building Materials",  
  10103: "Chemicals",  
  10104: "Coal",  
  10105: "Forest Products",  
  10106: "Metals & Mining",  
  10107: "Steel",  
  10208: "Advertising & Marketing Services",  
  10209: "Autos",  
  10210: "Entertainment",  
  10211: "Homebuilding & Construction",  
  10212: "Manufacturing - Apparel & Furniture",  
  10213: "Packaging & Containers",  
  10214: "Personal Services",  
  10215: "Publishing",  
  10216: "Restaurants",  
  10217: "Retail - Apparel & Specialty",  
  10218: "Travel & Leisure",  
  10319: "Asset Management",  
  10320: "Banks",  
  10321: "Brokers & Exchanges",  
  10322: "Credit Services",  
  10323: "Insurance",  
  10324: "Insurance - Life",  
  10325: "Insurance - Property & Casualty",  
  10326: "Insurance - Specialty",  
  10427: "Real Estate Services",  
  10428: "REITs",  
  20529: "Beverages - Alcoholic",  
  20530: "Beverages - Non-Alcoholic",  
  20531: "Consumer Packaged Goods",  
  20532: "Education",  
  20533: "Retail - Defensive",  
  20534: "Tobacco Products",  
  20635: "Biotechnology",  
  20636: "Drug Manufacturers",  
  20637: "Health Care Plans",  
  20638: "Health Care Providers",  
  20639: "Medical Devices",  
  20640: "Medical Diagnostics & Research",  
  20641: "Medical Distribution",  
  20642: "Medical Instruments & Equipment",  
  20743: "Utilities - Independent Power Producers",  
  20744: "Utilities - Regulated",  
  30845: "Communication Services",  
  30946: "Oil & Gas - Drilling",  
  30947: "Oil & Gas - E&P",  
  30948: "Oil & Gas - Integrated",  
  30949: "Oil & Gas - Midstream",  
  30950: "Oil & Gas - Refining & Marketing",  
  30951: "Oil & Gas - Services",  
  31052: "Aerospace & Defense",  
  31053: "Airlines",  
  31054: "Business Services",  
  31055: "Conglomerates",  
  31056: "Consulting & Outsourcing",  
  31057: "Employment Services",  
  31058: "Engineering & Construction",  
  31059: "Farm & Construction Machinery",  
  31060: "Industrial Distribution",  
  31061: "Industrial Products",  
  31062: "Transportation & Logistics",  
  31063: "Truck Manufacturing",  
  31064: "Waste Management",  
  31165: "Application Software",  
  31166: "Communication Equipment",  
  31167: "Computer Hardware",  
  31168: "Online Media",  
  31169: "Semiconductors"  
}
```

