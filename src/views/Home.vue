<template>
  <div>
    <h1>Welcome</h1>
    <button @click="getParsedData()">Generate</button>
  </div>
</template>
<script>
import parser from "cron-parser";
import moment from "moment";
export default {
  data() {
    return {};
  },
  mounted() {
    console.log(moment());
  },
  methods: {
    getParsedData() {
      var options = {
        currentDate: moment().toDate(),
        endDate: moment()
          .add(1, "days")
          .toDate(),
        iterator: true
      };

      console.log(options);

      try {
        var interval = parser.parseExpression("*/25 * * * *", options);

        while (true) {
          try {
            var obj = interval.next();
            console.log("value:", obj.value.toString(), "done:", obj.done);
          } catch (e) {
            break;
          }
        }

        // value: Wed Dec 26 2012 14:44:00 GMT+0200 (EET) done: false
        // value: Wed Dec 26 2012 15:00:00 GMT+0200 (EET) done: false
        // value: Wed Dec 26 2012 15:22:00 GMT+0200 (EET) done: false
        // value: Wed Dec 26 2012 15:44:00 GMT+0200 (EET) done: false
        // value: Wed Dec 26 2012 16:00:00 GMT+0200 (EET) done: false
        // value: Wed Dec 26 2012 16:22:00 GMT+0200 (EET) done: true
      } catch (err) {
        console.log("Error: " + err.message);
      }
    }
  }
};
</script>
