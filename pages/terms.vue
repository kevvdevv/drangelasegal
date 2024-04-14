<template>
  <div class="page-container terms-page">
    <div class="container-920">
      <h1 class="heading-style mb-24">Terms</h1>
      <div class="page-content">
        <div class="rte">
          <SanityContent :blocks="data.content" />
        </div>
      </div>
    </div>
  </div>
</template>
  <script>

export default {
  head() {
    let dsApiClient = new docusign.ApiClient();
    dsApiClient.setBasePath(docusign_base_uri);
    dsApiClient.addDefaultHeader('Authorization', 'Bearer ' + args.accessToken);
    let envelopesApi = new docusign.EnvelopesApi(dsApiClient);

    // Step 1. create the NDSE view
    let viewRequest = makeConsoleViewRequest(args);
    // Call the CreateSenderView API
    // Exceptions will be caught by the calling function
    let results = await envelopesApi.createConsoleView(args.accountId, {
      consoleViewRequest: viewRequest,
    });
    let url = results.url;
  },
};
</script>


  
  