<template>
  <div id="table">
    <div class="header">
      <strong>From <img class="svg-icon" style="height: 5px" src="../assets/icon_arrow01.svg" alt=""></strong> | To | Subject | Date
    </div>
    <div class="items">
      <div class="item" v-for="(mail, idx) in mails" :key="idx">
        <div class="info-wrapper">
          <img class="svg-icon" src="../assets/icon_mail_sp.svg" alt="">
          <div class="info">
            <div class="from"><strong>{{mail.from}}</strong><div class="date"><img v-if="mail.hasAttach" class="svg-icon mr-2" style="height: 16px" src="../assets/icon_clip.svg" alt="">{{mail.dateTime}}<img class="svg-icon ml-2" style="height: 10px" src="../assets/icon_arrow02.svg" alt=""></div></div>
          <div class="to"><span>{{mail.to.join(", ")+ (getTo(mail.to) ? ",..." : "")}}</span><div v-if="getTo(mail.to)" class="count">+{{getTo(mail.to)}}</div></div>
          </div>
        </div>
        <div class="subject">{{mail.subject}}</div>
        <div class="body is-truncated"><i>{{mail.body}}</i></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: "TableMobile",
    props: {
      mails: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        getTo(to) {
        if(to.length > 1) {
            return to.length - 1;
        } else {
            return false;
        }
        },
    }
}
</script>

<style lang="scss" scoped>
#table {
  background-color: #fff;
}
.header {
  border-top: solid 1px grey;
  border-bottom: solid 1px grey;
  background-color:  #dddddd7a;
  padding: 10px 20px !important;
  font-weight: 500;
  color: grey;
}

.item {
  padding: 10px 20px;
  border-bottom: solid 1px grey;

  .info-wrapper {
    display: flex;
    align-items: center;
    > img {
      height: 30px;
      margin: 6px 6px 0 0;
    }
    .info {
      width: 94%;
    }
  }

  .from, .to{
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .from {
    .date {
      display: flex;
      align-items: center;
    }
  }

  .to span, .subject {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    width: 90%;
  }

  .to {
    .count {
      line-height: initial;
      border: solid 1px;
      padding: 0;
      background-color: grey;
      color: #fff;
      border-radius: 5px;
      font-weight: 500;
      width: 25px;
      text-align: center;
      font-size: 12px;
    }
  }
}
</style>