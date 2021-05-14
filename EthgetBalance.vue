<template>
  <div class="Method-Wrapper">
    <div class="Method-Wrapper__header "
      @click="toggleExpand">
      <div
        class="Method-Wrapper__header__type ">
        READ
      </div>
      <div class="Method-Wrapper__header__title">
        eth_getBalance
      </div>
      <div class="Method-Wrapper__header__description">
        Returns the balance of the account of given address.
      </div>
      <div class="Method-Wrapper__header__expand-button">
        <i class="fa fa-chevron-down fa-lg" v-if="!expanded"></i>
        <i class="fa fa-chevron-up fa-lg"  v-if="expanded"></i>
      </div>
    </div>
    <div class="Method-Wrapper__body "
      v-if="expanded">
      <div class="Method-Wrapper__body__request">
        <div class="Method-Wrapper__body__request__header">
          <div class="Method-Wrapper__body__request__header__title">Request</div>
          <button @click="switchRunMode" class="Button Button--try-button">
            <template v-if="!runMode">
              Try It Out
            </template>
            <template v-if="runMode">
              Cancel
            </template>
          </button>
        </div>
        <div class="Method-Wrapper__body__request__description">
          Returns the balance of the account of given address.
        </div>
        <div class="Method-Wrapper__body__request__input-parameters">
          <div class="Method-Wrapper__body__request__input-parameters__header">Input Parameters</div>
          <div class="Method-Wrapper__body__request__input-parameters__position-wrapper">
            <div class="Method-Wrapper__body__request__input-parameters__position-wrapper__header">1st Parameter Options</div>
            <div class="Method-Wrapper__body__request__input-parameters__position-wrapper__body">
              <div class="Method-Wrapper__body__request__input-parameters__position-wrapper__body__header">
                address
              </div>
              <div class="Markdown-Override">
                <p><strong>DATA</strong>, 20 Bytes - address to check for balance.</p>
              </div>
            </div>
            <div class="Method-Wrapper__body__request__input-parameters__position-wrapper__header">2nd Parameter Options</div>
            <div class="Method-Wrapper__body__request__input-parameters__position-wrapper__body">
              <div class="Method-Wrapper__body__request__input-parameters__position-wrapper__body__header">
                block
              </div>
              <div class="Markdown-Override">
                <p><strong>QUANTITY|TAG</strong> - integer block number, or the string \&quot;latest\&quot;, \&quot;earliest\&quot; or \&quot;pending\&quot;, see the default block parameter</p>
              </div>
            </div>
          </div>
        </div>
        <div class="Method-Wrapper__body__request__request-body">
          <div class="Method-Wrapper__body__request__request-body__header">
            <span v-if="!runMode">
            Sample Request Body
            </span>
            <span v-if="runMode">
            Try Out Request Body
            </span>
          </div>
          <div class="Method-Wrapper__body__request__request-body__code">
            <template v-if="!runMode">
              <pre>
                                <!-- todo : generate for the variable in the js as well-->
                                <code class="hljs">
&#123;
    <span class="hljs-attr">&quot;id&quot;</span>: <span class="hljs-number">1</span>,
    <span class="hljs-attr">&quot;jsonrpc&quot;</span>: <span class="hljs-string">&quot;2.0&quot;</span>,
    <span class="hljs-attr">&quot;method&quot;</span>: <span class="hljs-string">&quot;eth_getBalance&quot;</span>,
    <span class="hljs-attr">&quot;params&quot;</span>: [
        <span class="hljs-string">&quot;0xc94770007dda54cF92009BFF0dE90c06F603a09f&quot;</span>,
        <span class="hljs-string">&quot;latest&quot;</span>
    ]
&#125;
                                </code>
                            </pre>
            </template>
            <template v-if="runMode">
              <textarea class="Method-Wrapper__body__request__request-body__code__entry"
                v-model="tryRequest" spellcheck="false"></textarea>
            </template>
          </div>
        </div>
        <template v-if="runMode">
          <button class="Button Button--run-button" :disabled="requestPending" @click="runCall">
            <template v-if="requestPending">
              <div class="spinner-border spinner-border-sm"></div>
              Running Request
            </template>
            <template v-if="!requestPending">
              Run Request
            </template>
          </button>
        </template>
      </div>
      <div class="Method-Wrapper__body__response">
        <div class="Method-Wrapper__body__response__header">
          <div class="Method-Wrapper__body__response__header__title">
            Response
          </div>
        </div>
        <template v-if="!runMode">
          <div class="Method-Wrapper__body__response__response-results">
            <div class="row">
              <div class="col-2 Method-Wrapper__body__response__response-results__header">
                Code
              </div>
              <div class="col-10 Method-Wrapper__body__response__response-results__header">
                Response
              </div>
            </div>
            <div class="row">
              <div class="col-2">
                <div class="Method-Wrapper__body__response__response-results__rpc-response">
                  Success
                </div>
                <div class="Method-Wrapper__body__response__response-results__http-response">
                  (HTTP 200)
                </div>
              </div>
              <div class="col-10">
                <div>
                  <div class="Markdown-Override">
                    <p><strong>QUANTITY</strong> - integer of the current balance in wei.</p>
                  </div>
                  <pre>
                                        <code class="hljs">
&#123;
    <span class="hljs-attr">&quot;id&quot;</span>: <span class="hljs-number">1</span>,
    <span class="hljs-attr">&quot;jsonrpc&quot;</span>: <span class="hljs-string">&quot;2.0&quot;</span>,
    <span class="hljs-attr">&quot;method&quot;</span>: <span class="hljs-string">&quot;eth_getBalance&quot;</span>,
    <span class="hljs-attr">&quot;result&quot;</span>: <span class="hljs-string">&quot;0x0234c8a3397aab58&quot;</span>
&#125;
                                        </code>
                                    </pre>
                </div>
              </div>
            </div>
            <div class="row">
              <div class="col-2">
                <div class="Method-Wrapper__body__response__response-results__rpc-response">
                  -32602
                </div>
                <div class="Method-Wrapper__body__response__response-results__http-response">
                  (HTTP 500)
                </div>
              </div>
              <div class="col-10">
                <div>
                  <div class="Markdown-Override">
                    <p>Method parameters invalid.</p>
                  </div>
                  <pre>
                                        <code class="hljs">
&#123;
    <span class="hljs-attr">&quot;id&quot;</span>: <span class="hljs-number">1</span>,
    <span class="hljs-attr">&quot;jsonrpc&quot;</span>: <span class="hljs-string">&quot;2.0&quot;</span>,
    <span class="hljs-attr">&quot;method&quot;</span>: <span class="hljs-string">&quot;eth_getBalance&quot;</span>,
    <span class="hljs-attr">&quot;error&quot;</span>: &#123;
        <span class="hljs-attr">&quot;code&quot;</span>: <span class="hljs-number">-32602</span>,
        <span class="hljs-attr">&quot;message&quot;</span>: <span class="hljs-string">&quot;method parameters invalid&quot;</span>
    &#125;
&#125;
                                        </code>
                                    </pre>
                </div>
              </div>
            </div>
            <div class="row">
              <div class="col-2">
                <div class="Method-Wrapper__body__response__response-results__rpc-response">
                  -32603
                </div>
                <div class="Method-Wrapper__body__response__response-results__http-response">
                  (HTTP 500)
                </div>
              </div>
              <div class="col-10">
                <div>
                  <div class="Markdown-Override">
                    <p>Something unexpected happened.</p>
                  </div>
                  <pre>
                                        <code class="hljs">
&#123;
    <span class="hljs-attr">&quot;id&quot;</span>: <span class="hljs-number">34</span>,
    <span class="hljs-attr">&quot;jsonrpc&quot;</span>: <span class="hljs-string">&quot;2.0&quot;</span>,
    <span class="hljs-attr">&quot;method&quot;</span>: <span class="hljs-string">&quot;eth_getBalance&quot;</span>,
    <span class="hljs-attr">&quot;error&quot;</span>: &#123;
        <span class="hljs-attr">&quot;code&quot;</span>: <span class="hljs-number">-32603</span>,
        <span class="hljs-attr">&quot;message&quot;</span>: <span class="hljs-string">&quot;Internal server error&quot;</span>
    &#125;
&#125;
                                        </code>
                                    </pre>
                </div>
              </div>
            </div>
          </div>
        </template>
        <template v-if="runMode">
          <template v-if="responseResult">
            <div class="Method-Wrapper__body__response__response-results">
              <div class="row">
                <div class="col-2">
                  Code
                </div>
                <div class="col-10">
                  Response
                </div>
              </div>
              <div class="row">
                <div class="col-2">
                  <div class="Method-Wrapper__body__response__response-results__rpc-response">
                    <template v-if="responseResult.ok">
                      {{responseResult.statusText}}
                    </template>
                    <template v-if="!responseResult.ok">
                      <template v-if="responseResult.errorCode">
                        {{responseResult.errorCode}}
                      </template>
                    </template>
                  </div>
                  <div v-if="responseResult.status"
                    class="Method-Wrapper__body__response__response-results__http-response">
                    (HTTP {{responseResult.status}})
                  </div>
                </div>
                <div class="col-10">
                  <div>
                    <pre v-highlightjs="sentResponseCode">
                                        <code class="json"></code>
                                    </pre>
                  </div>
                </div>
              </div>
            </div>
          </template>
          <template v-if="!responseResult">
            <div class="Method-Wrapper__body__response__try-response">
              <div v-if="!requestPending">
                Click on "Run" to run the request.
              </div>
              <div v-if="requestPending">
                <div class="spinner-border spinner-border-lg"></div>
                <div>Running Request</div>
              </div>
            </div>
          </template>
        </template>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
  import { Component, Prop, Vue } from 'vue-property-decorator';
  import axios from 'axios';
  import { COMMON_JSON_RPC_VALUES, INDENT_LENGTH_JSON_STRINGIFY } from '../constants';
  
  @Component
  export default class EthgetBalance extends Vue {
    private expanded: boolean = false;
    public runMode: boolean = false;
  
    public tryRequest: string = '';
    public ranOnce: boolean = false;
    public requestPending: boolean = false;
    public responseResult: any | null = null;
    public sentResponseCode: string | null = null;
  
    public methodType = 'READ';
    public methodName = 'eth_getBalance';
  
    public requestExample = ["{ \"params\": [\"0xc94770007dda54cF92009BFF0dE90c06F603a09f\", \"latest\"] }\n"];
  
    public toggleExpand(){
      this.expanded = !this.expanded;
    }
  
    switchRunMode() {
      this.runMode = !this.runMode;
  
      if (this.runMode && !this.ranOnce) {
        this.tryRequest = this.processJson(this.requestExample[0]);
      }
  
      this.ranOnce = true;
    }
  
    runCall() {    
      const methodType: any = this.methodType;
  
      switch (methodType) {
        case 'WRITE':
          this.runWriteTransaction(this.tryRequest);
          break;
        case 'READ':
          this.runReadTransaction(this.tryRequest);
          break;
        default:
          alert('Unsupported type');
          break;
      }
    }
  
    processJson(json) {
      const parsed = JSON.parse(json);
      const processed = {
          ...COMMON_JSON_RPC_VALUES,
          method: this.methodName,
          ...parsed
      };
      return JSON.stringify(processed, null, INDENT_LENGTH_JSON_STRINGIFY);
    }
  
    runReadTransaction(requestBody) {
      this.responseResult = null;
      this.requestPending = true;
      
      const options = {
          headers: {'content-type': 'application/json'}
      };
      axios.post(Vue.prototype.$readHostUrl, requestBody, options)
        .then((response) => {
          this.requestPending = false;
          this.responseResult = {
              statusText: 'Success',
              status: response.status,
              ok: true,
            };
          this.sentResponseCode = JSON.stringify(response.data, null, INDENT_LENGTH_JSON_STRINGIFY);
        })
        .catch(error => {
          this.requestPending = false;
          try {
            const parsedErrorBody = JSON.parse(error.request.response);
            this.responseResult = {
              errorCode: parsedErrorBody.error.code,
              ok: false,
            };
            this.sentResponseCode = JSON.stringify(parsedErrorBody.error, null, INDENT_LENGTH_JSON_STRINGIFY);
          }
          catch(e) {
            console.error('The following error occurred while parsing the json');
            console.log(e);
  
            this.responseResult = {
              errorCode: 'Unknown',
              ok: false,
            };
            this.sentResponseCode = '';
          }
        });
      }
  
      runWriteTransaction(request) {
        const web3Ethereum = Vue.prototype.$web3Result;
        if (web3Ethereum == null) {
          alert('There is no wallet connected, please connect your wallet');
          return;
        }
  
        this.responseResult = null;
        this.requestPending = true;
  
        try {
          const processedRequest = JSON.parse(request);
  
          web3Ethereum.request(processedRequest)
              .then(txnHash => {
                  this.requestPending = false;
                  this.responseResult = {
                      ok: true,
                      statusText: 'Success'
                  };
                  this.sentResponseCode = txnHash;
              })
              .catch(errorResponse => {
                  try {
                      this.requestPending = false;
  
                      // Convert to the type our frontend can read
                      this.responseResult = {
                          errorCode : (errorResponse && errorResponse.code)
                              ? errorResponse.code
                              : 'Unknown',
                          ok: false,
                      };
                      this.sentResponseCode = JSON.stringify(errorResponse, null, INDENT_LENGTH_JSON_STRINGIFY);
                  }
                  catch(e) {
                      this.processWriteUnknownError(e, 'An unknown error occurred locally on the browser while processing the error response');
                  }
              });
          }
          catch(e) {
              this.processWriteUnknownError(e, 'An unknown error occurred locally on the browser while processing the request');
          }
      }
  
      private processWriteUnknownError(e, errorString) {
          console.error(e);
              this.requestPending = false;
              this.responseResult = {
                  errorCode: 'Unknown',
                  ok: false,
              };
              this.sentResponseCode = errorString;
      }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import '../styles/details-entry.scss';
</style>