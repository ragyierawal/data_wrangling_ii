reading\_data\_from\_the\_web.Rmd
================
Ragyie Rawal
10/19/2021

## NSDUH data

``` r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

drug_use_html = read_html(url)

drug_use_df = 
  drug_use_html %>% 
  html_table() %>% 
  first() %>% 
  slice(-1)
```

## Star wars

Let’s get some star wars data

``` r
sw_url = "https://www.imdb.com/list/ls070150896/"

sw_html = read_html(sw_url)

# use CSS selector 
sw_titles = 
  sw_html %>% 
  html_elements(".lister-item-header a") %>% 
  html_text()

sw_revenue = 
  sw_html %>% 
  html_elements(".text-muted .ghost~ .text-muted+ span") %>% 
  html_text()

sw_df = 
  tibble(
    title = sw_titles,
    revenue = sw_revenue
  )
```

## Napolean Dynamite

``` r
dynamite_url = "https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber=1"

dynamite_html = 
  read_html(dynamite_url)

review_titles = 
  dynamite_html %>% 
  html_elements(".a-text-bold span") %>%
  html_text()

review_stars = 
  dynamite_html %>%
  html_elements("#cm_cr-review_list .review-rating") %>%
  html_text()

dynamite_df =
  tibble(
    titles = review_titles,
    stars = review_stars)
```
