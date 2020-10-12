<template>
  <div>
    <div class="content-wrap">
      <div class="calc-inner">
        <div class="calc-questions">
          <div class="question-wrap">
            <input name="ads-budget" type="number" min="100" max="50000" step="100" class="input-number" v-model="adsbudget">
            <h4 class="question-title">Estimated Monthly Budget</h4>
            <p><strong>How much do you or are you planning on spending each month on paid ads?</strong><br>
             If you are just kicking tires, simply test out a number. The industry average is 10% of your monthly marketing budget.</p>
            <div class="input-range-wrap currency">
              <input class="input-range" name="ads-budget" v-model="adsbudget" type="range" value="2000" min="100" max="50000" step="100">
              <div class="input-label-wrap">
                <p class="input-label">100</p>
                <p class="input-label">50k</p>
              </div>
            </div>
          </div>
          <div class="question-wrap">
            <input name="expectedcpc" type="number" min="0.1" max="50" step="0.1" class="input-number" v-model="expectedcpc">
            <h4 class="question-title">Estimated CPC</h4>
            <p><strong>How much do you estimate each click will cost you in your area?</strong><br>
             Depending on the ad network, and audience your CPC (Cost-Per-Click) can range from $2 to $30+.</p>
            <div class="input-range-wrap currency">
              <input class="input-range" name="expectedcpc" v-model="expectedcpc" type="range" min="0.1" max="50" step="0.1">
              <div class="input-label-wrap">
                <p class="input-label">0.1</p>
                <p class="input-label">50</p>
              </div>
            </div>
          </div>
          <div class="question-wrap">
            <input name="targetconversion" type="number" min="0.1" max="50" step="0.1" class="input-number" v-model="targetconversion">
            <h4 class="question-title">Target Conversion Rate</h4>
            <p><strong>How often does a visitor convert into a lead on your website?</strong><br>
             For the average practice it is around 3-5%.</p>
            <div class="input-range-wrap percent">
              <input class="input-range" name="targetconversion" v-model="targetconversion" type="range" min="0.1" max="50" step="0.1">
              <div class="input-label-wrap">
                <p class="input-label">0.1</p>
                <p class="input-label">50</p>
              </div>
            </div>
          </div>
          <div class="question-wrap">
            <input name="avgprice" type="number" min="100" max="100000" step="100" class="input-number" v-model="avgprice">
            <h4 class="question-title">Average Patient Value (Lifetime of Patient)</h4>
            <p><strong>On average, how valuable is a single customer?</strong><br>
              For many practices this will depend on what type of service you are advertising for. In general the LTV for a traditional dental patient is $5000. For more specific treatments like Dental Implants, or Invisalign you can use the average one-time gross treatment cost.</p>
            <div class="input-range-wrap currency">
              <input class="input-range" name="avgprice" v-model="avgprice" type="range" min="100" max="100000" step="100">
              <div class="input-label-wrap">
                <p class="input-label">100</p>
                <p class="input-label">100k</p>
              </div>
            </div>
          </div>
          <div class="question-wrap">
            <input name="custrate" type="number" min="1" max="90" step="1" class="input-number" v-model="custrate">
            <h4 class="question-title">What percentage of your leads turn into Customers?</h4>
            <p><strong>What percentage of your leads turn into Customers?</strong><br>
             This is critical to monitor. Talk to your front-desk and make sure the leads you receive are top-notch and well qualified. The industry average is 20% for Lead to Patient conversion.</p>
            <div class="input-range-wrap percent">
              <input class="input-range" name="custrate" v-model="custrate" type="range" min="1" max="90" step="1">
              <div class="input-label-wrap">
                <p class="input-label">1</p>
                <p class="input-label">90</p>
              </div>
            </div>
          </div>
        </div>
        <div class="calc-results">
          <div class="result-box" ref="print">
            <div class="result-details">
              <div class="result-title">Results</div>
              <div class="result-subtitle">Number of Clicks</div>
              <div class="result-num" v-text="clicks"></div>
              <div class="result-subtitle">Number of Leads</div>
              <div class="result-num" v-text="leads"></div>
              <div class="result-subtitle">Cost-Per-Lead</div>
              <div class="result-num" v-text="costper"></div>
              <div class="result-subtitle">Value of Lead</div>
              <div class="result-num" v-text="leadvalue"></div>
              <div class="result-subtitle">Expected Revenue</div>
              <div class="result-num" v-text="expectedrev"></div>
              <div class="result-subtitle">Expected Profit</div>
              <div class="result-num" v-text="expectedprofit"></div>
            </div>
            <div class="return-percent-wrap">
              <div class="result-subtitle">Return on Ad Spend</div>
              <div class="result-num"><span v-text="returnpercent"></span>%</div>
            </div>
            <div class="result-actions">
              <div id="share-action" @click="share">
                <svg version="1.1" id="share-icon" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512.001 512.001" style="enable-background:new 0 0 512.001 512.001;" xml:space="preserve">
                  <path d="M404.99,344.077c-26.743,0-50.588,12.583-65.974,32.124l-154.093-88.964c3.888-9.662,6.049-20.198,6.049-31.236 c0-11.037-2.162-21.573-6.049-31.236l154.093-88.964c15.387,19.54,39.231,32.124,65.974,32.124 c46.297,0,83.962-37.666,83.962-83.962C488.952,37.666,451.288,0,404.99,0s-83.962,37.665-83.962,83.961 c0,11.038,2.163,21.576,6.052,31.24l-154.091,88.964c-15.387-19.542-39.233-32.127-65.978-32.127  c-46.297,0-83.962,37.666-83.962,83.962c0,46.296,37.665,83.962,83.962,83.962c26.745,0,50.591-12.585,65.978-32.127L327.08,396.8 c-3.889,9.664-6.052,20.201-6.052,31.24c0,46.297,37.665,83.961,83.962,83.961s83.962-37.665,83.962-83.961 C488.952,381.744,451.288,344.077,404.99,344.077z M404.99,23.808c33.169,0,60.155,26.985,60.155,60.153  c0,33.169-26.985,60.155-60.155,60.155c-33.169,0-60.155-26.986-60.155-60.155C344.836,50.792,371.822,23.808,404.99,23.808z M107.011,316.155c-33.169,0-60.155-26.986-60.155-60.155c0-33.169,26.985-60.155,60.155-60.155  c33.169,0,60.155,26.986,60.155,60.155C167.166,289.169,140.18,316.155,107.011,316.155z M404.99,488.192  c-33.169,0-60.155-26.985-60.155-60.153c0-33.169,26.985-60.155,60.155-60.155c33.169,0,60.155,26.986,60.155,60.155  C465.145,461.208,438.159,488.192,404.99,488.192z"/>
                  <path d="M107.011,220.606c-19.516,0-35.394,15.877-35.394,35.394c0,6.573,5.329,11.904,11.904,11.904s11.904-5.331,11.904-11.904  c0-6.389,5.197-11.586,11.586-11.586c6.574,0,11.904-5.331,11.904-11.904C118.915,225.936,113.585,220.606,107.011,220.606z"/>
                </svg>
                <span>Copy Share Link</span>
              </div>
              <div id="pdf-action" @click="downpdf">
                <svg version="1.1" id="pdf-icon" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve">
                  <path d="M444.875,109.792L338.208,3.125c-2-2-4.708-3.125-7.542-3.125h-224C83.135,0,64,19.135,64,42.667v426.667 C64,492.865,83.135,512,106.667,512h298.667C428.865,512,448,492.865,448,469.333v-352 C448,114.5,446.875,111.792,444.875,109.792z M341.333,36.417l70.25,70.25h-48.917c-11.76,0-21.333-9.573-21.333-21.333V36.417z M426.667,469.333c0,11.76-9.573,21.333-21.333,21.333H106.667c-11.76,0-21.333-9.573-21.333-21.333V42.667 c0-11.76,9.573-21.333,21.333-21.333H320v64C320,108.865,339.135,128,362.667,128h64V469.333z"/>
                  <path d="M310.385,313.135c-9.875-7.771-19.26-15.76-25.51-22.01c-8.125-8.125-15.365-16-21.656-23.5  c9.813-30.323,14.115-45.958,14.115-54.292c0-35.406-12.792-42.667-32-42.667c-14.594,0-32,7.583-32,43.688 c0,15.917,8.719,35.24,26,57.698c-4.229,12.906-9.198,27.792-14.781,44.573c-2.688,8.052-5.604,15.51-8.688,22.406 c-2.51,1.115-4.948,2.25-7.302,3.427c-8.479,4.24-16.531,8.052-24,11.594C150.5,370.177,128,380.844,128,401.906 c0,15.292,16.615,24.76,32,24.76c19.833,0,49.781-26.49,71.656-71.115c22.708-8.958,50.938-15.594,73.219-19.75 c17.854,13.729,37.573,26.865,47.125,26.865c26.448,0,32-15.292,32-28.115c0-25.219-28.813-25.219-42.667-25.219 C337.031,309.333,325.49,310.604,310.385,313.135z M160,405.333c-6.094,0-10.219-2.875-10.667-3.427  c0-7.563,22.552-18.25,44.365-28.583c1.385-0.656,2.792-1.313,4.219-1.99C181.896,394.563,166.052,405.333,160,405.333z M234.667,214.354c0-22.354,6.938-22.354,10.667-22.354c7.542,0,10.667,0,10.667,21.333c0,4.5-3,15.75-8.49,33.313  C239.135,233.75,234.667,222.698,234.667,214.354z M242.844,329c0.667-1.854,1.313-3.729,1.938-5.625  c3.958-11.875,7.521-22.542,10.698-32.146c4.427,4.875,9.198,9.865,14.313,14.979c2,2,6.958,6.5,13.563,12.135  C270.208,321.208,256.219,324.76,242.844,329z M362.667,334.552c0,4.792,0,6.781-9.896,6.844  c-2.906-0.625-9.625-4.583-17.917-10.229c3.01-0.333,5.229-0.5,6.479-0.5C357.094,330.667,361.563,332.208,362.667,334.552z"/>
                </svg>
                <span>Download PDF</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { jsPDF } from "jspdf";
import html2canvas from "html2canvas"

export default {
  name: 'App',
  metaInfo: {
    title: 'Estimate Your Paid Ads ROI Online | Paid Ad Calculator',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      {
        vmid: 'description',
        name: 'description',
        content: 'Ever wonder if you should be running paid ads? Find out what your ROI could be in seconds with our paid ad calculator.',
      }
    ]
  },
  data() {
    return {
      adsbudget: 100,
      expectedcpc: 5,
      targetconversion: 10,
      avgprice: 1000,
      custrate: 10
    }
  },
  created() {
    if(this.$route.query.budget) {
      this.adsbudget = this.$route.query.budget;
    }
    if(this.$route.query.cpc) {
      this.expectedcpc = this.$route.query.cpc;
    }
    if(this.$route.query.targetconv) {
      this.targetconversion = this.$route.query.targetconv;
    }
    if(this.$route.query.priceavg) {
      this.avgprice = this.$route.query.priceavg;
    }
    if(this.$route.query.rate) {
      this.custrate = this.$route.query.rate;
    }
  },
  computed: {
    clicks: function () {
      return (this.adsbudget / this.expectedcpc).toFixed() 
    },
    leads: function () {
      return ((this.clicks * this.custrate) / 100).toFixed()
    },
    costper: function () {
      return (this.expectedcpc * this.targetconversion).toFixed()
    },
    leadvalue: function () {
      return (this.avgprice * (this.targetconversion / 100)).toFixed()
    },
    expectedrev: function () {
      return (this.leads * this.leadvalue).toFixed()
    },
    expectedprofit: function () {
      return (this.expectedrev - this.adsbudget).toFixed()
    },
    returnpercent: function () {
      return ((this.expectedprofit / this.adsbudget) * 100).toFixed()
    },
    sharelink() {
      return `https://roi.roadsidedentalmarketing.com/?budget=${encodeURIComponent(this.adsbudget)}&cpc=${encodeURIComponent(this.expectedcpcp)}&targetconv=${encodeURIComponent(this.targetconversion)}&priceavg=${encodeURIComponent(this.avgprice)}&rate=${encodeURIComponent(this.custrate)}`;
    },
  },
  methods: {
    CreateShare: function(e) {
      this.copy = this.sharelink;
      e.clipboardData.setData("text/html", this.copy);
      e.clipboardData.setData("text/plain", this.copy);
      e.preventDefault();
    },
    share() {
      console.log("link copied");
      document.addEventListener("copy", this.CreateShare);
      document.execCommand("copy");
      document.removeEventListener("copy", this.CreateShare);
      let myToast = this.$toasted.show("Link Copied",{
        position: "top-center"
      });
      myToast.goAway(1000);
    },
    downpdf() {
      console.log("download");
      var doc = new jsPDF({
        orientation: 'p',
        unit: 'in',
        format: 'letter',
      });
      doc.setFontSize(24).setTextColor("#2c3e50").text("Paid Ads ROI Estimate", 0.5,1.0);
      doc.setLineWidth(0.01).setFillColor("#e84256").line(0.5, 1.1, 8.0, 1.1, 'F');
      doc.setFontSize(16).setTextColor("#353b48").text("Estimated Monthly Budget: $" + this.adsbudget, 0.5,1.75);
      doc.setFontSize(16).setTextColor("#353b48").text("Estimated CPC: " + this.expectedcpc, 0.5,2.15);
      doc.setFontSize(16).setTextColor("#353b48").text("Target Conversion Rate: " + this.targetconversion, 0.5,2.45);
      doc.setFontSize(16).setTextColor("#353b48").text("Average Patient Value: $" + this.avgprice, 0.5,2.75);
      doc.setFontSize(16).setTextColor("#353b48").text("Percentage to leads: " + this.custrate + "%", 0.5,3.05);
      doc.setFillColor("#f9f9f9").rect(5,1.3,3,6, 'F');
      doc.setFontSize(14).setTextColor("#353b48").text("Results:", 6.5, 1.75, {align: "center", maxWidth: 3});
      doc.setLineWidth(0.01).setFillColor("#b9b9b9").line(5.5, 1.85, 7.5, 1.85, 'F');
      doc.setFontSize(12).setTextColor("#353b48").text("Number of Clicks", 6.5, 2.2, {align: "center", maxWidth: 3});
      doc.setFontSize(16).setTextColor("#353b48").text(this.clicks, 6.5, 2.5, {align: "center", maxWidth: 3});
      doc.setFontSize(12).setTextColor("#353b48").text("Number of Leads", 6.5, 3, {align: "center", maxWidth: 3});
      doc.setFontSize(16).setTextColor("#353b48").text(this.leads, 6.5, 3.3, {align: "center", maxWidth: 3});
      doc.setFontSize(12).setTextColor("#353b48").text("$" + "Cost-Per-Lead", 6.5, 3.8, {align: "center", maxWidth: 3});
      doc.setFontSize(16).setTextColor("#353b48").text(this.costper, 6.5, 4.1, {align: "center", maxWidth: 3});
      doc.setFontSize(12).setTextColor("#353b48").text("$" + "Value of Lead", 6.5, 4.6, {align: "center", maxWidth: 3});
      doc.setFontSize(16).setTextColor("#353b48").text(this.leadvalue, 6.5, 4.9, {align: "center", maxWidth: 3});
      doc.setFontSize(12).setTextColor("#353b48").text("$" + "Expected Revenue", 6.5, 5.4, {align: "center", maxWidth: 3});
      doc.setFontSize(16).setTextColor("#353b48").text(this.expectedrev, 6.5, 5.7, {align: "center", maxWidth: 3});
      doc.setFontSize(12).setTextColor("#353b48").text("Expected Profit", 6.5, 6.2, {align: "center", maxWidth: 3});
      doc.setFontSize(16).setTextColor("#353b48").text("$" + this.expectedprofit, 6.5, 6.5, {align: "center", maxWidth: 3});
      doc.setFillColor("#e84256").rect(5,7,3,1, 'F');
      doc.setFontSize(16).setTextColor("#FFFFFF").text("Return on Ad Spend", 6.5, 7.4, {align: "center", maxWidth: 3});
      doc.setFont("Helvetica", "bold").setFontSize(24).setTextColor("#FFFFFF").text(this.returnpercent + "%", 6.5, 7.8, {align: "center", maxWidth: 3});
      doc.save();
    }
  }
}
</script>