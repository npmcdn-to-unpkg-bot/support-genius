# SupportGenius

SupportGenius turns support tickets into valuable customer insights. Designed for customer success and support managers in data-driven organizations, SupportGenius leverages the power of machine learning to predict how customer and agent actions influence each other and identify similar customers. This, along with statistics such as the most common times that tickets are submitted, allows users to make smarter decisions about customer success and support strategy.  

## Technical Stack
PostgreSQL, Scikit-learn, NumPy, D3.js, Highcharts.js, Python fake-factory, Python, SQLAlchemy, Flask, JavaScript, jQuery, jQueryUI, AJAX, HTML/CSS, Bootstrap, Mashape Text-Processing API (Sentiment Analysis API)
 
## Data
This is an enterprise software application. In this demo, the data represents the support tickets from October 2015 for a fictitious company that sells to businesses. Thus, the data is reandomly created.
- Ticket contents were generated using Markov chains in Python creating new text snippets from separate positive and negative text files
- Agent names are members of Hackbright Cohort 12
- Company names were created using a [random company name generator](http://online-generator.com/name-generator/company-name-generator.php)
- Customer names were randomly generated using the [Python fake-factory library](https://pypi.python.org/pypi/fake-factory)
- Ticket submission, first response, and resolution times were randomly generated using Python fake-factory library 
- Agents were randomly assigned to tickets; customers were randomly assigned to companies, roles, and tickets; and companies were randomly assigned to different locations, support tiers, and industries. 
**Note: since the data was created randomly, it does not demonstrate strong linear relationships between the independent and dependent variables. Were this data real support data, there may be a stronger linear relationship or not, depending on a number of factors specifc to the organization, the structure of their support team, and their customers**


## Features
### D3.js: Ticket Data Graphs
- Heatmap of tickets per hour per day with the darkest boxes having the most tickets submitted
![ticket heatmap]
(https://cloud.githubusercontent.com/assets/13442273/11617349/6d91f932-9c42-11e5-89dd-0f77ef5c8bcb.png)
- Tickets by industry and tickets by support tier (Gold, Silver, or Bronze with Gold being the highest tier; represents the customer's purchased customer success plan) graphs 
![pie charts]
(https://cloud.githubusercontent.com/assets/13442273/11617369/9bcaebf6-9c42-11e5-9d91-caaaa2695676.png)
- Submitting a form with a the desired date range for tickets makes an AJAX call to render the appropriate graphs for that date range

### Highcharts.js: Scikit-learn Machine Learning Graphs
-  **Linear regression calculated using scikit-learn: Ticket submission time and response time**
![response time regression]
(https://cloud.githubusercontent.com/assets/13442273/11617377/ce2a396c-9c42-11e5-9cad-f7057a0279f3.png)
    * Shows the realationship between the time of day a ticket is submitted (the independent variable) and the time it takes an agent to respond to the ticket (the dependent variable)
    * Contains tooltips showing the x and y values for each scatter point
    * Drawn using Highcharts.js as it facilitates linear regression graphs
- **Linear regression calculated using scikit-learn: Agent-customer interactions and resolution time**
![agent touches resolution]
(https://cloud.githubusercontent.com/assets/13442273/11617388/144bf3fe-9c43-11e5-9439-87d125d03c0e.png)
    * Shows the relationship between the number of agent touches (the number of times the agent reaches out to a customer) and the amount of time it takes to resolve the ticket
    * Contains tooltips showing the x and y values for each scatter point
    * Drawn using Highcharts.js as it facilitates linear regression graphs
- **Meanshift calculated using scikit-learn: Customer clustering**
![meanshift bar graph]
(https://cloud.githubusercontent.com/assets/13442273/11617232/d21bfa08-9c40-11e5-9349-1cb47772ee60.png)
    * Shows the tickets separated into clusters based on the industry, support tier, and location of the company submitting the ticket; whether or not the company submitting the ticket is a pilot; the agent assigned to the ticket; and the sentiment of the ticket's text according to the text processing API.
    * Contains tooltips showing the total number of positive, negative, and neutral tickets in each cluster

### jQuery UI: Cluster Information Box
![cluster info]
(https://cloud.githubusercontent.com/assets/13442273/11617306/b4b89362-9c41-11e5-9a0d-41dda5355fc9.png)
- Box with tabs provides a drilldown into the contents of the clusters identified by the Meanshift algorithm
- The average percent negative of negative tickets and average percent positive of positive tickets is the average percent certainty that the ticket is positive or negative as determined by the Mashape Text-Processing API

### Bootstrap: Ticket Tables and Views
![main ticket view]
(https://cloud.githubusercontent.com/assets/13442273/11616046/a4a89d58-9c25-11e5-9a16-05ecd367e479.png)
- Additionally, view tickets in three different views by clicking the views menu:
    * **Agent View**
    ![agent view]
    (https://cloud.githubusercontent.com/assets/13442273/11617427/d6138d30-9c43-11e5-9c0f-ade6776efbaf.png)
        * Shows information about the agent assigned to the ticket
        * Shows all of the tickets assigned to that agent 
        * Can switch to another agent view by selecting another agent from the pull down menu
        * Allows managers insight into the productivity and success of their agents
    * **Company View**
    ![company view]
    (https://cloud.githubusercontent.com/assets/13442273/11617592/13566d82-9c46-11e5-9515-224d04106b15.png)
        * Shows information about a company that has submitted a ticket 
        * Shows all of the tickets associated with that company
        * Can switch to another company view by selecting another company from the pull down menu
        * Allows managers insight into the health of their company's relationships with customers and a drilldown into the specifics of each company
    * **Requester View**
    ![requester view]
    (https://cloud.githubusercontent.com/assets/13442273/11617676/2940d14a-9c47-11e5-82f0-b34fa4a065e1.png)
        * Shows information about a ticket requester
        * Shows all of the tickets that the requester has submitted
        * Can switch to another requester view by selecting another requester from the pull down menu
        * Allows managers to see 1) if problems with an account can be isolated to a single individual within that organization 2) if certain individuals/ roles within organizations need more education on the product 3) if certain individuals are likely to cause problems within the larger customer ecosystem
    
- All bootstrap tables showing tickets built using Jinja templates that allow the tables to update dynamically with information from the database; this allows the tables to update with additional data when it is added. 

### PostgreSQL Database
- SupportGenius is a product intended for the enterprise. Large companies that have millions of users will receive thousands of tickets in an hour. 
- PostgreSQL provides enterprise-scaling capeabilities, making it an excellent choice for this app

### Testing
- Included doc string tests; working on unit tests

## Next Steps
- Deployment on Heroku
- Dig into clusters to see customers in each cluster and get more data for each group of customers; see all the tickets for each cluster
- Calculate which customers are at risk of discontinuing the service
- Notifications to managers and agents when a ticket from an at-risk customer is submitted

