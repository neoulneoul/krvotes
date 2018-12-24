<!-- README.md is generated from README.Rmd. Please edit that file -->
Korean Votes
============

The goal of `krvotes` is to provide the Korean votes information.

Installation
------------

You can install the devloping version of `krvotes` from
[github](https://github.com/statkclee/krvotes) with:

``` r
# install.packages('remotes')
remotes::install_github("statkclee/krvotes")
```

Example - Presidential Election in 2017
---------------------------------------

``` r
# load package
library(krvotes)
suppressMessages(library(tidyverse))

# read presidential votes 2018 and assign it to president_df
president_df <- president
# check the structure of the object
str(object = president_df)
#> Classes 'tbl_df', 'tbl' and 'data.frame':    18455 obs. of  11 variables:
#>  $ 시도명  : chr  "서울특별시" "서울특별시" "서울특별시" "서울특별시" ...
#>  $ 구시군명: chr  "종로구" "종로구" "종로구" "종로구" ...
#>  $ 읍면동명: chr  "거소·선상투표" "관외사전투표" "재외투표" "청운효자동" ...
#>  $ 투표구명: chr  "거소·선상투표" "관외사전투표" "재외투표" "관내사전투표" ...
#>  $ 선거인수: num  218 12803 2490 1784 2493 ...
#>  $ 투표수  : num  206 12803 1813 1784 1682 ...
#>  $ 문재인  : num  64 5842 987 819 664 ...
#>  $ 홍준표  : num  42 2025 215 331 451 ...
#>  $ 안철수  : num  65 2509 304 352 342 ...
#>  $ 유승민  : num  8 1156 75 120 107 ...
#>  $ 심상정  : num  15 1145 214 149 96 ...
```

Example - local Election in 2018
--------------------------------

### Provicial Governor

``` r
local_2018_df <- local_2018

jeju_df <- local_2018_df %>%
  filter(str_detect(precinct, "제주")) %>%
  pull(data_clean) %>%
  .[[1]]

jeju_df %>%
  summarize(`문대림` = sum(democracy))
#> # A tibble: 1 x 1
#>   문대림
#>    <dbl>
#> 1 137901
```

### Mayor and County Governor

``` r
local_sigungu_df <- local_sigungu_2018

changwon_df <- local_sigungu_df %>% 
  filter(str_detect(precinct, "창원")) %>% 
  select(data_clean) %>% 
  unnest()

changwon_df %>% 
  filter(str_detect(sigungu, "성산")) %>% 
  summarise(허성무 = sum(`더불어민주당 허성무`),
            조진래 = sum(`자유한국당 조진래`),
            정규헌  = sum(`바른미래당 정규헌`),
            석영철  = sum(`민중당 석영철`),
            안상수  = sum(`무소속 안상수`),
            이기우  = sum(`무소속 이기우`))
#> # A tibble: 1 x 6
#>   허성무 조진래 정규헌 석영철 안상수 이기우
#>    <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
#> 1  68023  29669   3202   4139  16282   2782
```

-   [중앙선거관리위원회 - 선거통계시스템](http://info.nec.go.kr/)

역대선거 → 지방선거 → 제7회 → 구시군의 장선거 → 경상남도 → 창원시 →
창원시성산구

| 후보                | 득표수 |
|---------------------|--------|
| 더불어민주당 허성무 | 68,023 |
| 자유한국당 조진래   | 29,669 |
| 바른미래당 정규헌   | 3,202  |
| 민중당 석영철       | 4,139  |
| 무소속 안상수       | 16,282 |
| 무소속 이기우       | 2,782  |
