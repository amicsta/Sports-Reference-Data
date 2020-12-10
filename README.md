# Sports-Reference-Data
#Code to pull game logs off of Sports Reference as well as physical data
#html scrape sports ref
#2000 to 2019
library(htmltab)
t1 <- htmltab("https://www.sports-reference.com/cfb/play-index/pgl_finder.cgi?request=1&match=game&year_min=2000&year_max=2019&conf_id=&school_id=&opp_id=&game_type=&game_num_min=&game_num_max=&game_location=&game_result=&class=&c1stat=rec&c1comp=gt&c1val=0&c2stat=pass_att&c2comp=gt&c2val=0&c3stat=rush_att&c3comp=gt&c3val=0&c4stat=punt_ret&c4comp=gt&c4val=0&order_by=kick_ret&order_by_asc=&offset=0", which = 1, rm_nodata_cols = F, fillNA = 0, colNames = c("rk", "player", "date", "game_no", "school", "home_away", "opponent", "result", "pass_comp", "pass_att", "pass_pct", "pass_yd", "pass_td", "pass_int", "pass_rate", "rush_att", "rush_yd", "rush_avg", "rush_td", "rec_rect", "rec_yd", "rec_avg", "rec_td", "kr_ret", "kr_yd", "kr_avg", "kr_td", "pr_ret", "pr_yd", "pr_avg", "pr_td"))
t1[,c(9:31)] <- lapply(t1[,c(9:31)], as.numeric)
t1 <- na.omit(t1)

for (i in 1:8661) {
    a <- i*100
    url <- paste("https://www.sports-reference.com/cfb/play-index/pgl_finder.cgi?request=1&match=game&year_min=2000&year_max=2019&conf_id=&school_id=&opp_id=&game_type=&game_num_min=&game_num_max=&game_location=&game_result=&class=&c1stat=rec&c1comp=gt&c1val=0&c2stat=pass_att&c2comp=gt&c2val=0&c3stat=rush_att&c3comp=gt&c3val=0&c4stat=punt_ret&c4comp=gt&c4val=0&order_by=kick_ret&order_by_asc=&offset=",a,sep = "")
    t2 <- htmltab(url, which = 1, rm_nodata_cols = F, fillNA = 0, colNames = c("rk", "player", "date", "game_no", "school", "home_away", "opponent", "result", "pass_comp", "pass_att", "pass_pct", "pass_yd", "pass_td", "pass_int", "pass_rate", "rush_att", "rush_yd", "rush_avg", "rush_td", "rec_rect", "rec_yd", "rec_avg", "rec_td", "kr_ret", "kr_yd", "kr_avg", "kr_td", "pr_ret", "pr_yd", "pr_avg", "pr_td"))
t2[,c(9:31)] <- lapply(t2[,c(9:31)], as.numeric)
t2 <- na.omit(t2)
t1 <- rbind(t1,t2)
}
