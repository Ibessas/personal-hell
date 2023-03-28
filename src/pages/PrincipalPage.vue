<template>
  <div class="q-pa-xl">
    <div class="principal column flex-center">
      <p class="text-h3">Fullstack Developer</p>
      <div class="about">
        Software Engineer | Fullstack Developer | NodeJs | VueJs | Flutter | AWS
        | Java
      </div>
    </div>
    <div>
      <span class="text-h5"> Israel Bessa Silva </span>
      <div class="row socials">linkedin | instagram</div>
    </div>
    <div class="xp">
      <q-timeline color="secondary" layout="dense">
        <q-timeline-entry heading> Experience </q-timeline-entry>
        <div v-for="(item, index) in experiences" :key="index">
          <q-timeline-entry
            v-if="item.job"
            :title="item.job"
            :subtitle="getSubtitle(item)"
            :body="item.description"
          >
            <div></div>
          </q-timeline-entry>
        </div>
      </q-timeline>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      experiences: [
        {
          job: "Full Stack Developer",
          company: "Cupom Verde S/A",
          startDate: new Date("2021-04-01"),
          endDate: null,
          jobType: "Remote",
          regime: "CLT",
          description:
            "I act as Tech Lead of a Squad, helping with the questions of the squad and other collaborators, doing code review and teaching them about the technologies used and product processes. I also help other company employees to acquire analytical data about the product and do technical analysis on new features to be developed.",
          stack: [
            "Node 11",
            "Javascript",
            "Flutter 3",
            "Mysql",
            "Vue",
            "Quasar Framework",
            "Docker",
            "AWS",
            "Google Analytics",
            "Google Cloud",
            "Firebase",
            "Jira",
            "Discord",
            "Wordpress",
            "Serverless",
            "Jest",
            "Cypress",
            "Flutter Test",
            "Agile",
            "Pair Programming",
          ],
        },
        {
          job: "Full Stack Developer",
          company: "QuickData S/A",
          startDate: new Date("2021-05-01"),
          endDate: new Date("2021-07-01"),
          jobType: "Remote",
          regime: "CLT",
          description:
            "After the project Cupom Verde left Casa Magalhães, it moved to QuickData, before becoming its own company.",
          stack: [
            "Node",
            "Vue",
            "Flutter",
            "AWS",
            "Serverless",
            "Firebase",
            "Mysql",
            "Slack",
            "Zendesk",
            "Movides",
            "Youtrack",
            "Jest",
            "Bitrise",
            "Agile",
          ],
        },
        {
          job: "Developer",
          company: "Grupo Casa Magalhães ",
          startDate: new Date("2020-04-01"),
          endDate: new Date("2021-04-01"),
          jobType: "Remote",
          regime: "CLT",
          description:
            "The first company I worked for after college, I started there as a monitor for interns who were selected in a workshop held by Casa Magalhães. There I worked on several projects, where in the end I was assigned to the MVP of Coupon Verde, which after validation became a company. After some time working as a monitor, I became a junior developer, and before leaving Casa Magalhães I was promoted to developer.",
          stack: [
            "Node",
            "Vue",
            "Flutter",
            "AWS",
            "Serverless",
            "Firebase",
            "Mysql",
            "Slack",
            "Zendesk",
            "Movides",
            "Youtrack",
            "Jest",
            "Bitrise",
            "Agile",
          ],
        },
        {
          job: "Full Stack Developer",
          company: "Núcleo de Práticas em Informatica",
          startDate: new Date("2019-01-01"),
          endDate: new Date("2019-12-01"),
          jobType: "On-site",
          regime: "Intern",
          description:
            "At NPI, I worked as an intern developing internal systems for UFC.",
          stack: [
            "Vue",
            "Springboot",
            "Rest",
            "Postgresql",
            "Trello",
            "Gitlab",
          ],
        },
        {
          job: "",
          company: "",
          startDate: new Date("2021-05-01"),
          endDate: new Date("2021-07-01"),
          jobType: "",
          description: "",
          stack: [],
        },
      ],
    };
  },
  methods: {
    getYearMonth(date) {
      const auxDate = new Date(date);
      return `${auxDate.getFullYear()}/${this.getLeftZero(
        auxDate.getMonth() + 1
      )}`;
    },
    getSubtitle(exp) {
      const { startDate, endDate } = exp;
      return `${this.getYearMonth(startDate)} - ${
        endDate ? this.getYearMonth(endDate) : "Present"
      }`;
    },
    getLeftZero(number) {
      const stringNumber = `${number}`;
      return stringNumber.length == 1 ? `0${stringNumber}` : stringNumber;
    },
  },
};
</script>
<style lang="sass">
.principal
  height: 70vh
.xp
  margin-top: 15vh
</style>
