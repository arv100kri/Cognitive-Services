<!-- 
NavPath: Web Language Model API
LinkLabel: Overview
Url: web-language-model-api/documentation
Weight: 100
-->

# Web Language Model API Overview

Welcome to the Microsoft Project Oxford Web Language Model API, a REST-based cloud service providing state-of-the-art tools for natural language processing. Using this API, your application can leverage the power of big data through language models trained on web-scale corpora collected by Bing in the EN-US market. 

These smoothed backoff N-gram language models, supporting Markov order up to 5, are trained on the following corpora: 

- Web page body text 
- Web page title text 
- Web page anchor text 
- Web search query text 

The Web LM REST API supports four lookup operations:

1. Joint (log10) probability of a sequence of words.  
2. Conditional (log10) probability of one word given a sequence of preceding words. 
3. List of words (completions) most likely to follow a given sequence of words. 
4. Word breaking of strings that contain no spaces. 

## Getting Started

1. Subscribe to the service [here](http://www.microsoft.com/cognitive-services/en-us/subscriptions?productId=/products/55e3f82f778daf16b4ba484c).
2. Download the [SDK](https://github.com/Microsoft/ProjectOxford-ClientSDK/tree/master/WebLM).
3. Run the SDK sample code. 
4. Consult the [API Reference](https://dev.projectoxford.ai/docs/services/55de9ca4e597ed1fd4e2f104) for further details, including code snippets in a variety of languages.
