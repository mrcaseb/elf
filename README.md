
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Unofficial Data Repo of the European League of Football <img src="logo.png" align="right" width="25%" min-width="120px"/>

## Preface

This repo hosts play-by-play and other stats data of the European League
of Football (ELF).

The following data is available:

-   `games` file that includes all games, corresponding `game_ids` (in
    the format `season_week_awayteam_hometeam`) and results.
-   `pbp` files that provide some basic play-by-play data
-   `stats` files that provide team based total stats per game
-   `raw_xml` files from the ELF api

Please note that some raw\_xml files might miss in the api completely or
might miss relevant data. Since everything is quite new this can change
quickly.

## How to Load the Data

All data is available in two file formats: `*.rds` (the native binary R
format) and `*.csv` (comma separated lists that can be used with any
software). The following code blocks demonstrate how to load the data
with R.

We use a helper function to load rds files through the internet:

``` r
rds_from_url <- function(url){
  con <- url(url)
  on.exit(close(con))
  readRDS(con)
}
```

### Load Games

``` r
# Load .rds file
games_rds <- rds_from_url("https://github.com/mrcaseb/elf/blob/master/data/elf_games.rds?raw=true")
# Load .csv file
games_csv <- readr::read_csv("https://raw.githubusercontent.com/mrcaseb/elf/master/data/elf_games.csv", col_types = readr::cols())
# Preview output information
dplyr::glimpse(games_rds)
#> Rows: 40
#> Columns: 12
#> $ season       <dbl> 2021, 2021, 2021, 2021, 2021, 2021, 2021, 2021, 2021, 202~
#> $ week         <dbl> 1, 1, 1, 1, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 5, 5, 5, 6, 6, ~
#> $ game_id      <glue> "2021_01_SS_BD", "2021_01_CC_PW", "2021_01_FG_HD", "2021~
#> $ api_id       <chr> "bdss2101", "pwcc2101", "hdfg2101", "btlk2101", "pwlk2102~
#> $ home_team    <chr> "Barcelona Dragons", "Panthers Wroclaw", "Hamburg Sea Dev~
#> $ away_team    <chr> "Stuttgart Surge", "Cologne Centurions", "Frankfurt Galax~
#> $ home_team_id <chr> "BD", "PW", "HD", "BT", "PW", "CC", "SS", "LK", "BD", "FG~
#> $ away_team_id <chr> "SS", "CC", "FG", "LK", "LK", "BD", "FG", "CC", "HD", "PW~
#> $ home_score   <dbl> 17, 55, 17, 27, 54, 40, 20, 47, 14, 22, 40, NA, NA, NA, N~
#> $ away_score   <dbl> 21, 39, 15, 37, 28, 12, 42, 48, 32, 13, 19, NA, NA, NA, N~
#> $ result       <dbl> -4, 16, 2, -10, 26, 28, -22, -1, -18, 9, 21, NA, NA, NA, ~
#> $ total        <dbl> 38, 94, 32, 64, 82, 52, 62, 95, 46, 35, 59, NA, NA, NA, N~
```

### Load Stats

``` r
# Load .rds file
stats_rds <- rds_from_url("https://github.com/mrcaseb/elf/blob/master/data/elf_team_stats.rds?raw=true")
# Load .csv file
stats_csv <- readr::read_csv("https://raw.githubusercontent.com/mrcaseb/elf/master/data/elf_team_stats.csv", col_types = readr::cols())
# Preview output information
dplyr::glimpse(stats_rds)
#> Rows: 20
#> Columns: 123
#> $ game_id                <glue> "2021_01_SS_BD", "2021_01_SS_BD", "2021_01_CC_~
#> $ team_name              <chr> "Stuttgart Surge", "Barcelona Dragons", "Cologn~
#> $ team_id                <chr> "SS", "BD", "CC", "PW", "FG", "HD", "LK", "BT",~
#> $ type                   <chr> "away", "home", "away", "home", "away", "home",~
#> $ record                 <chr> "1-0-0", "0-1-0", "0-1-0", "1-0-0", "0-1-0", "1~
#> $ abb                    <chr> "S", "B", "C", "P", "F", "H", "L", "B", NA, "B"~
#> $ firstdowns_no          <chr> "15", "17", "19", "28", "22", "9", "18", "17", ~
#> $ firstdowns_rush        <chr> "5", "4", "6", "11", "5", "6", "4", "4", NA, "3~
#> $ firstdowns_pass        <chr> "8", "10", "12", "17", "12", "3", "10", "10", N~
#> $ firstdowns_penalty     <chr> "2", "3", "1", "0", "5", "0", "4", "3", NA, "4"~
#> $ penalties_no           <chr> "10", "13", "7", "7", "5", "11", "12", "13", NA~
#> $ penalties_yds          <chr> "134", "149", "52", "67", "40", "117", "160", "~
#> $ conversions_thirdconv  <chr> "1", "4", "3", "5", "5", "4", "4", "3", NA, "6"~
#> $ conversions_thirdatt   <chr> "8", "11", "12", "12", "11", "11", "11", "14", ~
#> $ conversions_fourthconv <chr> "0", "0", "2", "0", "0", "0", "1", "2", NA, "1"~
#> $ conversions_fourthatt  <chr> "2", "1", "4", "1", "0", "0", "2", "3", NA, "3"~
#> $ fumbles_no             <chr> "0", "0", "1", "3", "5", "1", "0", "1", NA, "0"~
#> $ fumbles_lost           <chr> "0", "0", "1", "2", "2", "0", "0", "1", NA, "0"~
#> $ misc_yds               <chr> "6", "0", "-51", "3", "-4", "0", "0", "4", NA, ~
#> $ misc_top               <chr> "27:58", "31:56", "00:00", "00:00", "35:30", "2~
#> $ misc_ona               <chr> "0", "0", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ misc_onm               <chr> "0", "0", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ misc_ptsto             <chr> "0", "0", "13", "17", "3", "7", "0", "9", NA, "~
#> $ redzone_att            <chr> "3", "3", "0", "0", "4", "1", "4", "4", NA, "1"~
#> $ redzone_scores         <chr> "2", "1", "0", "0", "3", "1", "4", "4", NA, "0"~
#> $ redzone_points         <chr> "15", "7", "0", "0", "15", "3", "26", "21", NA,~
#> $ redzone_tdrush         <chr> "1", "0", "0", "0", "1", "0", "0", "0", NA, "0"~
#> $ redzone_tdpass         <chr> "1", "1", "0", "0", "1", "0", "4", "3", NA, "0"~
#> $ redzone_fgmade         <chr> "0", "0", "0", "0", "1", "1", "0", "1", NA, "0"~
#> $ redzone_endfga         <chr> "0", "0", "0", "0", "1", "0", "0", "0", NA, "0"~
#> $ redzone_enddowns       <chr> "1", "1", "0", "0", "0", "0", "0", "0", NA, "1"~
#> $ redzone_endint         <chr> "0", "1", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ redzone_endfumb        <chr> "0", "0", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ redzone_endhalf        <chr> "0", "0", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ redzone_endgame        <chr> "0", "0", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ rush_att               <chr> "23", "22", "31", "34", "23", "27", "21", "20",~
#> $ rush_yds               <chr> "105", "93", "264", "162", "83", "105", "67", "~
#> $ rush_gain              <chr> "127", "100", "280", "189", "87", "114", "76", ~
#> $ rush_loss              <chr> "22", "7", "16", "27", "4", "9", "9", "5", NA, ~
#> $ rush_td                <chr> "1", "0", "3", "1", "1", "0", "0", "0", NA, "0"~
#> $ rush_long              <chr> "27", "16", "72", "34", "8", "17", "21", "17", ~
#> $ pass_comp              <chr> "14", "19", "18", "24", "29", "8", "22", "18", ~
#> $ pass_att               <chr> "25", "29", "35", "43", "36", "16", "39", "33",~
#> $ pass_int               <chr> "1", "1", "3", "0", "1", "1", "2", "1", NA, "2"~
#> $ pass_yds               <chr> "99", "222", "220", "364", "177", "80", "206", ~
#> $ pass_td                <chr> "2", "2", "2", "5", "1", "1", "4", "4", NA, "2"~
#> $ pass_long              <chr> "40", "46", "28", "45", "17", "29", "40", "83",~
#> $ pass_sacks             <chr> "0", "4", "1", "2", "4", "2", "1", "8", NA, "3"~
#> $ pass_sackyds           <chr> "0", "32", "10", "20", "28", "8", "9", "46", NA~
#> $ rcv_no                 <chr> "14", "19", "18", "24", "29", "8", "22", "18", ~
#> $ rcv_yds                <chr> "99", "254", "220", "364", "205", "88", "215", ~
#> $ rcv_td                 <chr> "2", "2", "2", "5", "1", "1", "4", "4", NA, "2"~
#> $ rcv_long               <chr> "40", "46", "28", "45", "17", "29", "40", "83",~
#> $ punt_no                <chr> "4", "3", "3", "3", "4", "6", "4", "4", NA, "6"~
#> $ punt_yds               <chr> "93", "50", "108", "93", "130", "268", "154", "~
#> $ punt_long              <chr> "39", "43", "43", "37", "37", "69", "47", "41",~
#> $ punt_blkd              <chr> "1", "0", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ punt_tb                <chr> "0", "0", "0", "0", "0", "1", "0", "0", NA, "0"~
#> $ punt_fc                <chr> "0", "1", "0", "1", "0", "1", "0", "0", NA, "0"~
#> $ punt_plus50            <chr> "0", "0", "0", "0", "0", "2", "0", "0", NA, "0"~
#> $ punt_inside20          <chr> "2", "0", "0", "2", "0", "3", "2", "0", NA, "1"~
#> $ punt_avg               <chr> "23.2", "16.7", "36.0", "31.0", "32.5", "44.7",~
#> $ ko_no                  <chr> "5", "3", "7", "10", "4", "4", "6", "7", NA, "3~
#> $ ko_yds                 <chr> "283", "171", "260", "561", "259", "250", "312"~
#> $ ko_ob                  <chr> "0", "2", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ ko_tb                  <chr> "0", "0", "0", "0", "2", "2", "0", "3", NA, "0"~
#> $ ko_fcyds               <chr> "0", "0", "0", "0", "0", "0", "0", "0", NA, "0"~
#> $ pat_kickatt            <chr> "2", "1", "5", "7", "1", "2", "3", "1", NA, "1"~
#> $ pat_kickmade           <chr> "1", "1", "3", "7", "0", "2", "3", "0", NA, "0"~
#> $ pat_passatt            <chr> "1", "1", "1", NA, "1", NA, "2", "3", NA, NA, N~
#> $ pat_passmade           <chr> "1", "1", "0", NA, "0", NA, "0", "0", NA, NA, N~
#> $ pat_rcvatt             <chr> "1", "1", NA, NA, NA, NA, NA, NA, NA, NA, NA, N~
#> $ pat_rcvmade            <chr> "1", "1", NA, NA, NA, NA, NA, NA, NA, NA, NA, N~
#> $ defense_tackua         <chr> "29", "21", "52", "43", "26", "36", "37", "28",~
#> $ defense_tacka          <chr> "22", "12", "2", "22", "24", "34", "18", "26", ~
#> $ defense_tot_tack       <chr> "51", "33", "54", "65", "50", "70", "55", "54",~
#> $ defense_tflua          <chr> "4", "5", "6", "2", "5", "5", "9", "2", NA, "1"~
#> $ defense_tfla           <chr> "8", "4", "0", "6", "0", "4", "8", "6", NA, "0"~
#> $ defense_tflyds         <chr> "41", "68", "34", "18", "13", "33", "54", "18",~
#> $ defense_sacks          <chr> "4", "0", "2", "1", "2", "4", "8", "1", NA, "0"~
#> $ defense_sackyds        <chr> "32", "0", "20", "10", "8", "28", "46", "9", NA~
#> $ defense_brup           <chr> "3", "3", "3", "3", "3", "2", "3", "3", NA, NA,~
#> $ defense_blkd           <chr> "1", "1", NA, "1", NA, NA, "1", NA, NA, NA, "1"~
#> $ defense_int            <chr> "1", "1", NA, "3", "1", "1", "1", "2", NA, NA, ~
#> $ defense_intyds         <chr> "18", "0", NA, "87", "0", "0", "90", "33", NA, ~
#> $ kr_no                  <chr> "1", "5", "10", "7", "2", "2", "3", "6", NA, "3~
#> $ kr_yds                 <chr> "43", "133", "267", "84", "27", "56", "146", "2~
#> $ kr_td                  <chr> "0", "0", "0", "0", "0", "0", "1", "0", NA, "0"~
#> $ kr_long                <chr> "43", "60", "54", "30", "18", "30", "93", "89",~
#> $ ir_no                  <chr> "1", "1", NA, "3", "1", "1", "1", "2", NA, NA, ~
#> $ ir_yds                 <chr> "18", "0", NA, "87", "0", "0", "90", "33", NA, ~
#> $ ir_td                  <chr> "0", "0", NA, "1", "0", "0", "0", "0", NA, NA, ~
#> $ ir_long                <chr> "18", "0", NA, "45", "0", "0", "90", "33", NA, ~
#> $ scoring_td             <chr> "3", "2", "6", "7", "2", "2", "5", "4", NA, "2"~
#> $ scoring_patkick        <chr> "1", "1", "3", "7", NA, "2", "3", NA, NA, NA, "~
#> $ scoring_patrcv         <chr> "1", "1", NA, NA, NA, NA, NA, NA, NA, NA, NA, N~
#> $ fg_made                <chr> NA, "0", "0", "2", "1", "1", NA, "1", NA, NA, N~
#> $ fg_att                 <chr> NA, "3", "1", "3", "2", "1", NA, "1", NA, NA, N~
#> $ fg_long                <chr> NA, "0", "0", "34", "42", "33", NA, "33", NA, N~
#> $ fg_blkd                <chr> NA, "1", "0", "0", "0", "0", NA, "0", NA, NA, N~
#> $ defense_saf            <chr> NA, "1", NA, NA, NA, NA, "1", NA, NA, NA, NA, N~
#> $ pr_no                  <chr> NA, "1", "1", "2", "2", "2", "1", "2", NA, "3",~
#> $ pr_yds                 <chr> NA, "11", "0", "19", "11", "17", "0", "9", NA, ~
#> $ pr_td                  <chr> NA, "0", "0", "0", "0", "0", "0", "0", NA, "0",~
#> $ pr_long                <chr> NA, "0", "0", "14", "11", "17", "0", "7", NA, "~
#> $ scoring_saf            <chr> NA, "1", NA, NA, NA, NA, "1", NA, NA, NA, NA, N~
#> $ defense_ff             <chr> NA, NA, "2", "1", NA, "1", "1", NA, NA, NA, NA,~
#> $ defense_fr             <chr> NA, NA, "2", "1", NA, "2", "1", NA, NA, "1", NA~
#> $ defense_fryds          <chr> NA, NA, "0", "0", NA, "43", "0", NA, NA, "0", N~
#> $ fr_no                  <chr> NA, NA, "0", NA, NA, "1", NA, NA, NA, NA, NA, N~
#> $ fr_yds                 <chr> NA, NA, "0", NA, NA, "43", NA, NA, NA, NA, NA, ~
#> $ fr_td                  <chr> NA, NA, "1", NA, NA, "1", NA, NA, NA, NA, NA, N~
#> $ fr_long                <chr> NA, NA, "0", NA, NA, "43", NA, NA, NA, NA, NA, ~
#> $ pat_retkatt            <chr> NA, NA, NA, "1", NA, NA, NA, NA, NA, NA, NA, NA~
#> $ pat_retkmade           <chr> NA, NA, NA, "0", NA, NA, NA, NA, NA, NA, NA, NA~
#> $ scoring_fg             <chr> NA, NA, NA, "2", "1", "1", NA, "1", NA, NA, NA,~
#> $ pat_retfatt            <chr> NA, NA, NA, NA, NA, NA, "1", NA, NA, NA, NA, NA~
#> $ pat_retfmade           <chr> NA, NA, NA, NA, NA, NA, "1", NA, NA, NA, NA, NA~
#> $ scoring_patretfumb     <chr> NA, NA, NA, NA, NA, NA, "1", NA, NA, NA, NA, NA~
#> $ pat_rushatt            <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, "1", NA, NA~
#> $ pat_rushmade           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, "0", NA, NA~
#> $ scoring_patrush        <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
#> $ scoring_patretkick     <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
```

### Load PBP

``` r
# Load .rds file
pbp_rds <- rds_from_url("https://github.com/mrcaseb/elf/blob/master/data/pbp/elf_pbp_2021.rds?raw=true")
# Load .csv file
pbp_csv <- readr::read_csv("https://raw.githubusercontent.com/mrcaseb/elf/master/data/pbp/elf_pbp_2021.csv", col_types = readr::cols())
# Preview output information
dplyr::glimpse(pbp_rds)
#> Rows: 1,763
#> Columns: 61
#> $ game_id          <glue> "2021_01_CC_PW", "2021_01_CC_PW", "2021_01_CC_PW", "~
#> $ away_team_id     <chr> "CC", "CC", "CC", "CC", "CC", "CC", "CC", "CC", "CC",~
#> $ home_team_id     <chr> "PW", "PW", "PW", "PW", "PW", "PW", "PW", "PW", "PW",~
#> $ away_team        <chr> "Cologne Centurions", "Cologne Centurions", "Cologne ~
#> $ home_team        <chr> "Panthers Wroclaw", "Panthers Wroclaw", "Panthers Wro~
#> $ date             <chr> "6/19/2021", "6/19/2021", "6/19/2021", "6/19/2021", "~
#> $ location         <chr> "Wroclaw, Poland", "Wroclaw, Poland", "Wroclaw, Polan~
#> $ stadium          <chr> "Stadion Olimpijski", "Stadion Olimpijski", "Stadion ~
#> $ start            <chr> "18:00", "18:00", "18:00", "18:00", "18:00", "18:00",~
#> $ end              <chr> "21:14", "21:14", "21:14", "21:14", "21:14", "21:14",~
#> $ leaguegame       <chr> "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y"~
#> $ nitegame         <chr> "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y"~
#> $ schednote        <chr> "W", "W", "W", "W", "W", "W", "W", "W", "W", "W", "W"~
#> $ duration         <chr> "3:14", "3:14", "3:14", "3:14", "3:14", "3:14", "3:14~
#> $ attend           <chr> "3000", "3000", "3000", "3000", "3000", "3000", "3000~
#> $ temp             <chr> "32C", "32C", "32C", "32C", "32C", "32C", "32C", "32C~
#> $ wind             <chr> "E 8km/h", "E 8km/h", "E 8km/h", "E 8km/h", "E 8km/h"~
#> $ weather          <chr> "Sunny", "Sunny", "Sunny", "Sunny", "Sunny", "Sunny",~
#> $ ref              <chr> "Walentynowicz", "Walentynowicz", "Walentynowicz", "W~
#> $ ump              <chr> "Klimes", "Klimes", "Klimes", "Klimes", "Klimes", "Kl~
#> $ line             <chr> "Walentynowicz", "Walentynowicz", "Walentynowicz", "W~
#> $ lj               <chr> "Pachulski", "Pachulski", "Pachulski", "Pachulski", "~
#> $ bj               <chr> "Simon", "Simon", "Simon", "Simon", "Simon", "Simon",~
#> $ fj               <chr> "Hameder", "Hameder", "Hameder", "Hameder", "Hameder"~
#> $ sj               <chr> "Kriesman", "Kriesman", "Kriesman", "Kriesman", "Krie~
#> $ posteam          <chr> "CC", "CC", "CC", "PW", "CC", "CC", "CC", "CC", "PW",~
#> $ down             <chr> "1", "1", "1", "1", "1", "2", "3", "4", "1", "2", "3"~
#> $ togo             <chr> "10", "10", "10", "10", "10", "7", "7", "7", "10", "1~
#> $ spot             <chr> "CC35", "CC35", "CC35", "PW35", "CC30", "CC33", "CC33~
#> $ context          <chr> "V,1,10,V35", "V,1,10,V35", "V,1,10,V35", "H,1,10,H35~
#> $ play_id          <chr> "0,1,0", "0,2,1", "0,3,3", "0,4,4", "1,1,5", "1,2,6",~
#> $ tokens           <chr> "SPOT:V,V35,N", "Q:1 T:00:00", "SPOT:H,H35,N", "KO:11~
#> $ desc             <chr> "CC ball on CC35.", "Start of 1st quarter, clock 00:0~
#> $ newcontext       <chr> "V,1,10,V35", "V,1,10,V35", "H,1,10,H35", "V,1,10,V30~
#> $ play_type        <chr> NA, NA, NA, "kick_off", "rush", "rush", "pass", "punt~
#> $ clock            <chr> NA, "00:00", NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
#> $ first_down_with  <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, "pass", NA, N~
#> $ oob              <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0,~
#> $ turnover         <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N~
#> $ score            <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
#> $ away_score_post  <chr> "0", "0", "0", "0", "0", "0", "0", "0", "0", "0", "0"~
#> $ home_score_post  <chr> "0", "0", "0", "0", "0", "0", "0", "0", "0", "0", "0"~
#> $ drive_number     <int> 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,~
#> $ drive_vh         <chr> NA, NA, NA, NA, "V", "V", "V", "V", "H", "H", "H", "H~
#> $ drive_team       <chr> NA, NA, NA, NA, "CC", "CC", "CC", "CC", "PW", "PW", "~
#> $ drive_start      <chr> NA, NA, NA, NA, "KO,1,00:00,30", "KO,1,00:00,30", "KO~
#> $ drive_end        <chr> NA, NA, NA, NA, "PUNT,1,00:00,33", "PUNT,1,00:00,33",~
#> $ drive_plays      <chr> NA, NA, NA, NA, "3", "3", "3", "3", "13", "13", "13",~
#> $ drive_yards      <chr> NA, NA, NA, NA, "3", "3", "3", "3", "61", "61", "61",~
#> $ drive_top        <chr> NA, NA, NA, NA, "0:00", "0:00", "0:00", "0:00", "0:00~
#> $ drive_start_how  <chr> NA, NA, NA, NA, "KO", "KO", "KO", "KO", "PUNT", "PUNT~
#> $ drive_start_qtr  <chr> NA, NA, NA, NA, "1", "1", "1", "1", "1", "1", "1", "1~
#> $ drive_start_time <chr> NA, NA, NA, NA, "00:00", "00:00", "00:00", "00:00", "~
#> $ drive_start_spot <chr> NA, NA, NA, NA, "CC30", "CC30", "CC30", "CC30", "PW38~
#> $ drive_end_how    <chr> NA, NA, NA, NA, "PUNT", "PUNT", "PUNT", "PUNT", "DOWN~
#> $ drive_end_qtr    <chr> NA, NA, NA, NA, "1", "1", "1", "1", "1", "1", "1", "1~
#> $ drive_end_time   <chr> NA, NA, NA, NA, "00:00", "00:00", "00:00", "00:00", "~
#> $ drive_end_spot   <chr> NA, NA, NA, NA, "CC33", "CC33", "CC33", "CC33", "CC01~
#> $ drive_rz         <chr> NA, NA, NA, NA, NA, NA, NA, NA, "1", "1", "1", "1", "~
#> $ cj               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N~
#> $ alt              <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N~
```
