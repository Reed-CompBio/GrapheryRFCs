# Workflows

## Tutorial Page Workflow

This subsection is dedicated to introduce the workflow in the tutorial page. The tutorial page is a page consisting of three sections: text section, graphing section, and code+variable section. This workflow is strongly connected to storage transaction, and as a result it controls data fetching, loading, and packaging. The purpose of this is to allow view components to use the packaged getters right away without worrying about processing.

- When the page is loaded, the event `fetch-tutorial` will be emitted, to signal the storage action to fetch tutorial content from the server. This event will command the storage to download the information of the tutorial, given the tutorial url and target language. The information contains the text content, code, and identifiers of graphs.

- Once the fetching action is executed, an `fetched-tutorial` event will then be emitted. It will also trigger several other events: `fetched-tutorial`, and subsequently and `load-code` if fetching is executed successfully.

- When `load-code` is dispatched, the current code id will be set to the proper code identifier, and a getter will automatically register  the proper code object so that the editor component can use.

- When the identifiers are loaded, the graph selector component will display available graphs and automatically try to fetch the first graph. (Since the fetched tutorial contains only the graph identifier instead of all information of the graph, the information has to be fetched in separate calls.)

- Along side of loading graph information, the execution record array is also fetched, installed into the storage, and served by a getter so that the frontend can display properly. Every time a new execution record is loaded, the record state will be reset by calling the `reset-state` event.
