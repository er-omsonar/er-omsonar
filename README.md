1.OM ATL 
#code 
library(shiny)

ui <- fluidPage(
  
  titlePanel("My First Shiny App"),
  
  sidebarLayout(
    position = "right",
    
    sidebarPanel(
      "This is the Sidebar Panel"
    ),
    
    mainPanel(
      "This is the Main Panel"
    )
  )
)

server <- function(input, output) {
  
}

shinyApp(ui = ui, server = server)



#Console command 
install.packages("shiny")
library(shiny)
