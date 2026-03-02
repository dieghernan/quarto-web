``` python
from great_tables import GT
from great_tables.data import countrypops
import polars as pl
import polars.selectors as cs

# Get vectors of 2-letter country codes for each region of Oceania
oceania = {
    "Australasia": ["AU", "NZ"],
    "Melanesia": ["NC", "PG", "SB", "VU"],
    "Micronesia": ["FM", "GU", "KI", "MH", "MP", "NR", "PW"],
    "Polynesia": ["PF", "WS", "TO", "TV"],
}

# Create a dictionary mapping country to region (e.g. AU -> Australasia)
country_to_region = {
    country: region for region, countries in oceania.items() for country in countries
}

wide_pops = (
    pl.from_pandas(countrypops)
    .filter(
        pl.col("country_code_2").is_in(list(country_to_region))
        & pl.col("year").is_in([2000, 2010, 2020])
    )
    .with_columns(pl.col("country_code_2").replace(country_to_region).alias("region"))
    .pivot(index=["country_name", "region"], columns="year", values="population")
    .sort("2020", descending=True)
)

(
    GT(wide_pops, rowname_col="country_name", groupname_col="region")
    .tab_header(title="Populations of Oceania's Countries in 2000, 2010, and 2020")
    .tab_spanner(label="Total Population", columns=cs.all())
    .fmt_integer()
)
```

    /var/folders/_5/l_f9_2dj4n5dpm0ztth7n97c0000gp/T/ipykernel_41564/3569039387.py:26: DeprecationWarning: The argument `columns` for `DataFrame.pivot` is deprecated. It has been renamed to `on`.
      .pivot(index=["country_name", "region"], columns="year", values="population")

| Populations of Oceania's Countries in 2000, 2010, and 2020 |  |  |  |
|----|----|----|----|
|  | Total Population |  |  |
|  | 2000 | 2010 | 2020 |
| Australasia |  |  |  |
| Australia | 19,028,802 | 22,031,750 | 25,655,289 |
| New Zealand | 3,857,700 | 4,350,700 | 5,090,200 |
| Melanesia |  |  |  |
| Papua New Guinea | 5,508,297 | 7,583,269 | 9,749,640 |
| Solomon Islands | 429,978 | 540,394 | 691,191 |
| Vanuatu | 192,074 | 245,453 | 311,685 |
| New Caledonia | 213,230 | 249,750 | 272,460 |
| Polynesia |  |  |  |
| French Polynesia | 250,927 | 283,788 | 301,920 |
| Samoa | 184,008 | 194,672 | 214,929 |
| Tonga | 102,603 | 107,383 | 105,254 |
| Tuvalu | 9,638 | 10,550 | 11,069 |
| Micronesia |  |  |  |
| Guam | 160,188 | 164,905 | 169,231 |
| Kiribati | 88,826 | 107,995 | 126,463 |
| Micronesia (Federated States) | 111,709 | 107,588 | 112,106 |
| Northern Mariana Islands | 80,338 | 54,087 | 49,587 |
| Marshall Islands | 54,224 | 53,416 | 43,413 |
| Palau | 19,726 | 18,540 | 17,972 |
| Nauru | 10,377 | 10,241 | 12,315 |
