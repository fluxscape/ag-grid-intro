First of all, Thanks to Eric Tuvesson

![image](https://github.com/user-attachments/assets/18704e7f-5e1f-4d1e-849d-91bdc176a29f)


Open the project, then navigate to the Home page.

https://www.loom.com/share/cc6fccdc9ddc45deba2811fe9da1b7fe
The script used:
let api = null;

Script.Signals.Setup = function () {
    // Define column definitions
    //Use the columns name in your class
    const columnDefs = [
        { field: "name" },
        { field: "objectId" },
        { field: "createdAt" },
        { field: "updatedAt" }
    ];

    // specify the data source and column definitions
    const gridOptions = {
        columnDefs: columnDefs,
        pagination: true,
        paginationPageSize: 50,
        rowModelType: 'infinite',
        datasource: {
            getRows: fetchData
        }
    };

    // initialize the grid passing in the div to use together with the columns & data we want to use
    const gridDiv = Script.Inputs.Node.getDOMElement();
    new agGrid.Grid(gridDiv, gridOptions);
}

// Fetch data from the server
async function fetchData(params) {
    // Construct the query
    const query = {};

    const options = {
        skip: params.startRow,
        limit: params.endRow - params.startRow,
        count: true,
    };

    try {
        // Make a request to your server-side API to fetch data
        //Important: set the query to the prefered column. "test. in this case"
        const response = await Noodl.Records.query("test", query, options);

        // Provide the fetched data to AG Grid
        params.successCallback(response.results, response.count);
    } catch (error) {
        console.error('Error fetching data:', error);
        params.failCallback();
    }
}

Here is the fluxscape, which you can paste into the editor:

{"nodes":[{"id":"7de5b3d8-12e1-f005-c432-d789ab3c2396","type":"Group","x":441,"y":62,"parameters":{"cssClassName":"ag-theme-alpine","styleCss":"/* background-color: red; */\n"},"ports":[],"children":[]},{"id":"22671267-13e0-221b-fbe5-be933647582a","type":"Javascript2","x":-271,"y":164,"parameters":{"code":"let api = null;\r\n\r\nScript.Signals.Setup = function () {\r\n    // Define column definitions\r\n    const columnDefs = [\r\n        { field: \"name\" },\r\n        { field: \"objectId\" },\r\n        { field: \"createdAt\" },\r\n        { field: \"updatedAt\" }\r\n    ];\r\n\r\n    // specify the data source and column definitions\r\n    const gridOptions = {\r\n        columnDefs: columnDefs,\r\n        pagination: true,\r\n        paginationPageSize: 50,\r\n        rowModelType: 'infinite',\r\n        datasource: {\r\n            getRows: fetchData\r\n        }\r\n    };\r\n\r\n    // initialize the grid passing in the div to use together with the columns & data we want to use\r\n    const gridDiv = Script.Inputs.Node.getDOMElement();\r\n    new agGrid.Grid(gridDiv, gridOptions);\r\n}\r\n\r\n// Fetch data from the server\r\nasync function fetchData(params) {\r\n    // Construct the query\r\n    const query = {};\r\n\r\n    const options = {\r\n        skip: params.startRow,\r\n        limit: params.endRow - params.startRow,\r\n        count: true,\r\n    };\r\n\r\n    try {\r\n        // Make a request to your server-side API to fetch data\r\n        const response = await Noodl.Records.query(\"test\", query, options);\r\n\r\n        // Provide the fetched data to AG Grid\r\n        params.successCallback(response.results, response.count);\r\n    } catch (error) {\r\n        console.error('Error fetching data:', error);\r\n        params.failCallback();\r\n    }\r\n}\r\n"},"ports":[],"children":[],"metadata":{"merge":{"soureCodePorts":["code"]}}}],"connections":[{"fromId":"7de5b3d8-12e1-f005-c432-d789ab3c2396","fromProperty":"didMount","toId":"22671267-13e0-221b-fbe5-be933647582a","toProperty":"Setup"},{"fromId":"7de5b3d8-12e1-f005-c432-d789ab3c2396","fromProperty":"this","toId":"22671267-13e0-221b-fbe5-be933647582a","toProperty":"Node"}],"comments":[{"text":"This script sets up an AG Grid within a Noodl.net low-code environment, defining column configurations and enabling pagination with infinite row model support. It initializes the grid using a specified HTML element and dynamically fetches data from a server using a provided API, ensuring the grid is populated with the fetched records. The script handles both successful data retrieval and errors during the data fetching process.","width":639,"height":276,"fill":"transparent","x":-731,"y":61,"id":"20f95813-0493-cba2-5915-1f1f1ef49bf7"},{"text":"Here the AG Grid will live - also check out the AG Themes:  https://www.ag-grid.com/react-data-grid/themes/","width":383,"height":70,"fill":"transparent","x":282,"y":165,"id":"8aa51c17-a237-52e7-7e0e-a155bc28c657"}]}
