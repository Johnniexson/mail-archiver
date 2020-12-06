<template>
  <table>
      <tr class="header">
        <th class="has-text-grey">From</th>
        <th class="has-text-grey">To</th>
        <th class="has-text-grey">Subject</th>
        <th><strong>Date <img class="svg-icon" src="../assets/icon_arrow01.svg" alt=""></strong></th>
      </tr>
      <tr class="item" v-for="(mail, idx) in mails" :key="idx">
        <td>{{mail.from}}</td>
        <td><span>{{mail.to[0]+ (getTo(mail.to) ? ",..." : "")}}<div v-if="getTo(mail.to)" class="count">+{{getTo(mail.to)}}</div></span></td>
        <td><span><span class="is-truncated p-0">{{mail.subject}}</span> <img v-if="mail.hasAttach" class="svg-icon" src="../assets/icon_clip.svg" alt=""></span>
        <div class="body">{{mail.body}}</div>
        </td>
        <td><strong>{{mail.dateTime}}</strong></td>
      </tr>
    </table>
</template>

<script>
export default {
    name: "TableList",
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
table {
  width: 100%;
  background-color: white;
  .header {
    border-top: solid 1px grey;
    background-color:  #dddddd7a;

    th:nth-child(2) {
      min-width: 20%;
    }

    th:last-child {
      strong {
        display: flex;
        align-items: baseline;

        img {
          height: 5px;
        }
      }
    }
  }

  tr {
    line-height: 50px;
    border-bottom: solid 1px grey;
  }

  tr :nth-child(1) {
      padding-left: 10px;
    }

  .item:hover {
    cursor: pointer;
    color: blue;
    background-color:  #dddddd6e;
  }

  .item td:nth-child(3) {
    line-height: 45px;
    max-width: 40%;
  }

  .item td:nth-child(3) > span {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0;
    font-weight: 600;
  }

  .item td:nth-child(3) > .body {
    color: grey;
    display: -webkit-box;
    -webkit-line-clamp: 1;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  .item td:nth-child(2) span {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-right: 50px;

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