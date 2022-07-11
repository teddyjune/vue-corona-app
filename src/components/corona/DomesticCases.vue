<template>
  <div>
    <ul class="graph-list">
      <li>
        <h3>누적 확진/사망자 추이</h3>
        <ChartGraph />
      </li>
    </ul>
  </div>
</template>

<script>
import ChartGraph from "../charts/ChartGraph";
import coronaMixin from "@/mixins/coronaMixin";
export default {
  name: "DomesticCases",
  mixins: [coronaMixin],
  components: { ChartGraph },

  data() {
    return {
      caseKey: 0,
      compareKey: 0,
      monthDifference: 5,
      domesticData: [],
    };
  },
  mounted() {
    this.fetchDomestic();
  },
  methods: {
    async fetchDomestic() {
      const url = "https://api.covid.com/live/country/south-korea";
      const domestic = await this.fetchData("get", url);
    },
  },
};
</script>

<style scoped>
.graph-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1em;
  list-style: none;
}
</style>
