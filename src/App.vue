<template>
  <div id="app">
    <div class="filter mb-4">
      <div class="field has-addons">
        <div class="control has-icons-left">
          <input class="is-hidden" color="grey" ref='calendarTrigger' type="date" data-is-range="true">
          <input class="input trigger" type="text" style="padding-left: 50px" v-model="dateRange" readonly>
          <span class="icon is-small is-left pl-4">
            <img class="svg-icon" src="./assets/icon_calender.svg" alt="">
          </span>
        </div>
        <div class="control">
          <a class="button search-btn has-bg-primary">
            <img class="svg-icon" src="./assets/icon_search.svg" alt="">
          </a>
        </div>
      </div>
    </div>

    <div class="header">
      <strong class="has-text-grey">Results: <span class="is-size-5">{{mails.length}}</span> mail(s)</strong>
    </div>

    <div class="mt-2">
      <tableMobile v-if="isMobile" :mails="mails" />
      <tableList v-else :mails="mails" />
    </div>
  </div>
</template>

<script>
import bulmaCalendar from 'bulma-calendar';
import tableList from './components/Table';
import tableMobile from './components/TableMobile';

export default {
  name: 'App',
  components: {
    tableList,
    tableMobile
  },
  data() {
    return {
      viewPort: screen.width,
      startDate: new Date(),
      endDate: new Date(),
      mails: [
        {
          from: "aaa@example.com",
          to: ["zzz.zzz@example.com"],
          subject: "[HR-888] Notice of official announcement",
          dateTime: "0:20",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: false
        },
        {
          from: "bbb.bbb@example.com",
          to: ["yyy@example.com"],
          subject: "[web:333] \"Web Contact\"",
          dateTime: "0:10",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: false
        },
        {
          from: "ccc@example.com",
          to: ["xxx@example.com","www.www@example.com"],
          subject: "Happy New Year! Greetings for the New year.",
          dateTime: "Jan 01",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: true
        },
        {
          from: "ddd.ddd@example.com",
          to: ["vvv.vvv@example.com","uuu@example.com"],
          subject: "[HR-887(Revised: Office Expansion Project Team)] Notice of off...",
          dateTime: "Jan 01",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: false
        },
        {
          from: "eee@example.com",
          to: ["sss@example.com","rr.rrr@example.com","d@d.com"],
          subject: "[Github] Logout page",
          dateTime: "Jan 01",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: false
        },
        {
          from: "fff.fff@example.com",
          to: ["qqq.qqq@example.com"],
          subject: "[dev] Postfix 3.1.12/3.2.9/3.3.4/3.4.5",
          dateTime: "Jan 01",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: false
        },
        {
          from: "ggg@example.com",
          to: ["ppp@example.com"],
          subject: "Re: [Github] Brush-up on loading animation",
          dateTime: "Jan 01",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: false
        },
        {
          from: "hhh.hhh@example.com",
          to: ["ooo.ooo@example.com"],
          subject: "Workplace Summary for sample, Inc.: Jun2 - Jun9",
          dateTime: "Jan 01",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: true
        },
        {
          from: "iii@example.com",
          to: ["nnn@example.com"],
          subject: "I love you",
          dateTime: "2019/12/31",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          hasAttach: true
        },
        {
          from: "Pablo-Diego-...",
          to: ["Pablo-Diego-Jose-Francisc..."],
          subject: "[info:888] ABC EQUIPMENT COMPANY",
          body: "lorem ipsum body, lorem ipsum is here to say hello",
          dateTime: "2019/12/31",
          hasAttach: false
        },
      ]
    }
  },
  mounted() {
    this.$nextTick(() => {
      window.addEventListener('resize', this.onResize);
    })

    const calendar = new bulmaCalendar(this.$refs.calendarTrigger, {
      startDate: this.startDate,
      endDate: this.endDate
    })
    calendar.on('select', e => {
      this.startDate = e.data.startDate
      this.endDate = e.data.endDate
    })
  },

  beforeDestroy() { 
    window.removeEventListener('resize', this.onResize); 
  },

  computed: {
    dateRange() {
      return `${this.formatDate(this.startDate) + " - " + this.formatDate(this.endDate)}`;
    },

    isMobile() {
      return this.viewPort < 400;
    }
  },
  
  methods: {
    formatDate(date) {
      return date.getFullYear() + "/" + (date.getMonth() + 1) + "/" + date.getDate()
    },

    onResize() {
      this.viewPort = screen.width;
    }
  }
}
</script>

<style lang="scss">
#app {
  min-height: 100vh;
  background-image: url("./assets/logo.png");
  background-repeat: no-repeat;
  background-position: center;
  margin: 50px 80px;
}

@media(max-width: "400px") {
  #app {
    margin: 20px 0;

    .filter, .header {
      padding: 0 20px;
    }
  }
}

.trigger {
  width: 240px;
  border-radius: 8px 0 0 8px !important;
}

.search-btn {
  border-radius: 0 8px 8px 0 !important;
}
</style>
