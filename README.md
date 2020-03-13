# daterangepicker

<!-- badges: start -->
[![Lifecycle: maturing](https://img.shields.io/badge/lifecycle-maturing-blue.svg)](https://www.tidyverse.org/lifecycle/#maturing)
<!-- badges: end -->

Custom Shiny input binding for a [Date Range Picker](https://www.daterangepicker.com/).

## Installation

``` r
remotes::install_github("trafficones/daterangepicker")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(shiny)
library(daterangepicker)

## UI ##########################
ui <- fluidPage(
  tags$head(tags$style(".myclass {
                        /*margin: 50px 0 0 507px;*/
                        background-color: #96dafb;}")),
  daterangepicker(
    inputId = "daterange",
    label = "Wählen Sie ein Datum aus",
    start = Sys.Date() - 30, end = Sys.Date(),
    max = as.character(Sys.Date()),
    language = "de",
    style = "width:100%; border-radius:4px",
    class = "myclass",
    icon = icon("calendar")
  ),
  verbatimTextOutput("print"),
  actionButton("act", "Update Daterangepicker"),
)

## SERVER ##########################
server <- function(input, output, session) {
  output$print <- renderPrint({
    req(input$daterange)
    input$daterange
  })
  observeEvent(input$act, {
    updateDaterangepicker(session, "daterange",
                          start = as.Date(Sys.Date()), 
                          end = as.Date(Sys.Date())-100)
  })
}

shinyApp(ui, server)
```

