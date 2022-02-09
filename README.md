# Financial Institution (SPA) Coding Challenge

![SPA Preview](https://i.ibb.co/Syk2c5H/screenshot-localhost-3000-2022-02-08-15-30-21.png)

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app) and feeds data locally via a JSON file that was provided. Care was taken to code key components utilities and functions so that they meet the coding challenge requirements while displaying a range of JavaScript coding skills. 

Due to time constraints this is a development version of the application and not a production ready SPA.

## Contents
- [Financial Institution (SPA) Coding Challenge](#financial-institution--spa--coding-challenge)
  * [Requirements](#requirements)
  * [Available Scripts](#available-scripts)
  * [Solution Analysis](#solution-analysis)
    + [General Layout](#general-layout)
    + [Provided data set](#provided-data-set)
    + [Libraries used](#libraries-used)
    + [Testing](#testing)
    + [Further development](#further-development)

## Requirements

 - Customers sorted by default in alphabetical order
 - As a user, when viewing my customer list, I expect to see:
	 - Full customer name
	 - Customer risk profile
	 - Aggregated customer net worth from all underlying portfolios
	 - Aggregated restriction status from all underlying portfolios
	 - Aggregated capital gain from all underlying portfolios
 - As a user, when viewing my customer list, I expect to be able to change their sorting by any of their displayed information fields
 - As a user, when drilling down into a customer’s specific investment portfolio, I expect to see a list of all the
assets included in that portfolio sorted by default in alphabetical order
 - As a user, when viewing the list of assets in a specific portfolio, I expect to see the following information for
each asset:
	 - Asset name, Asset type, Location, Quantity, Total Value, Capital Gain, Associated Risk
 - As a user, when viewing the list of assets in a specific portfolio, I expect to be able to change their sorting by any of their displayed information fields
 - As a user, I expect to be able to freely navigate between a selected portfolio and my client list so I can drill
down into a different client/portfolio
 - [x] Optional – As a user, when viewing my customer list, I expect to be able to filter it via a text input field
 - [x] Optional – As a user, when viewing the list of assets in a specific portfolio, I expect to be able to filter it via a text input field
 - [x] Optional – As a developer, to ensure consistency and durability of my solution, I will introduce some tests that can be run via the terminal of my IDE
 - [x] Optional – As a user, I would like the application to be responsive so I can use it on different devices
 - [x] Optional – As a user, I want a streamlined professional look to my application that is consistent throughout

## Available Scripts

To start the application, in the project directory, run:

 `npm install`
 `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits to the src code.\
You will also see any lint errors in the console.

 `npm test`

Launches the test runner in the interactive watch mode.\
See the library docs [running tests](https://testing-library.com/docs/react-testing-library/intro/) for more information.

## Solution Analysis

The following is a brief explanation of my solution to the coding challenge criteria that was provided.

**Note: This is not intended as a complete reference of how I would develop an application for a production-level project.**

### General Layout

To meet time constraints I used existing libraries to handle currencies and for clean and professional styling, I opted to create my own component and utilities. However as a self challenge and so as to meet the requirements as closely as possible.

General layout of the application was largely determined by the 'nested tables' requirement. The solution was made as an SPA so as to better demonstrate the expandability of the tables. Additionaly, each header element features both a sort arrow and a filtered search.

Data is fed row by row in to the table which by default is sorted by "Client Name". Use of the arrow icons `|-> & ⇅` allows for sorting and expanding the table to view the required fields.

By default the chart displays all available data, but can be filtered by typing in the search field. Results are  provided to the end user immediately.

All column headers were determined by the assignment and are as follows:
 - Client Name
 - Risk Profile
 - Net Worth
 - Restrictions
 - Capital Gain
	 - Portfolio #
	 - Restriction Status
		 - Asset
		 - Type
		 - Location
		 - Quantity
		 - Value
		 - Capital Gain
		 - Associated Risk

### Provided data set

Several small issues and features of the back-end were identified and handled in the JSON provided :

 - [x] capitalGainPerAsset is a String type
 - [x] clients can have identical names
 - [x] firstName lastName need to be concatenated
 - [x] assets are reported in multiple currencies 

**Assumptions:**
 - riskProfile is an int value of range unknown.
 - as we're dealing with currency in cents use of parseInt() is preferable to parseFloat()
 - all requested calculations should result in a currency format display. ie: Capital Gain, Associated Risk etc should be displayed as a currency in the table.
 - If tested on alternate JSON datasets <= max 300 clients, anymore would require implementation of pagination.

### Libraries used
Care was taken to streamline the application and load a minimum of libraries.

 - [dinero](https://dinerojs.com/) (gzipped: 3.3k)
	 - Upon researching money handling libraries for javascript I came across this library that not only performs above my expectations but provides every feature I could need to handle currency conversions, calculations and formatting.  
 - [react-bootstrap](https://react-bootstrap.github.io/) (gzipped: 2.3k)
	 - As the optional requirements needed a clean professional and responsive layout I opted for bootstrap, this allowed me to import the Container, Row, Col, Table, FormControl, with which i handled displaying and styling. 
 - [react-bootstrap-icons](https://www.npmjs.com/package/react-bootstrap-icons) (gzipped: 1.6k)
 - Easy and quick source of icons used for it's low size and high speed/performance.

Testing Library:

 - [react testing library](https://testing-library.com/docs/react-testing-library/intro/) (gzipped: 45.9k)
	 - Not only is it a light-weight and fast library, it also encourages better testing practices. It is not however a proper testing-framework like Jest and was chosen so as to meet the time constraints.

### Testing

Testing for this solution focuses primarily around end-to-end due to time constraints. Rendered elements are targetted using the getByText function which verifies if the element is present against an `expect(titleElement).toBeInTheDocument();` statement.

### Further development

Certain restrictions should be noted when taking this project into consideration which had i had different criteria or time constrains would have been done differently:

 - **Originally intended to use AG Grid data grid.** 
	 - However the nested tables with filtering is a [Enterprise](https://www.ag-grid.com/license-pricing.php) only feature. I therefore opted to use react-bootstrap and code from scratch the filters and sorting.
 - **Currency Handling - Dinero.js Library**
	 - While I've made use of the library to it's full extent to format and perform the math operations correctly I was unable to source a free currency API that allowed for a sufficient amount of requests to ensure it would always just work. This lead to my coding a USD > EUR rate conversion over the data fetched from the API, Ideally I would have preferred to have access to a full API so as to be able to include a const displayCurrency so that the application could easily be switched to a different currency. I chose not to use a prefabricated Json with rates so as to demonstrate my ability to correctly retrieve, map and manipulate data.  
 - **Optional Task Responsive**
	 - The optional responsive task has been met but has a min break point as I made the assumption that this sort of SPA would not be used in a financial setting on a mobile phone.

Had this been a full production-level application I would have preferred to also include the following:

 - Use a component library that would have provided me with more
   customization and styling options.
 - Dockerised the solution.
 - Introduce a login and authorization solution as well as client <-> backend security.
 - Introduce logic to make the SPA a full CRED (create - read - edit -delete) web app.
 - Theming and eye protection support.
 - Include Data visualizations for a better user experience.
 - Access the provided JSON files backend API or create a mock API for the SPA.
 - Refine the sorting/filtering logic so as to allow a sidebar for a neater UI.
 - Introduce logic for conditional formatting i.e red/green for currency and Capitalization for assetType etc.
 - Do more extensive testing and cover more use-scenarios.
