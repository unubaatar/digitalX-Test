<template>
  <div>
    <footer
      style="
        display: flex;
        justify-content: space-around;
        height: 200px;
        background-color: blue;
      "
    >
      <span>
        <img
          :src="userInfo.logoUrl"
          alt=""
          style="width: 150px; object-fit: contain"
        />
        <div style="text-align: center; font-size: 24px; color: white">
          {{ userInfo.domain }}
        </div>
      </span>
      <div style="margin-top: 16px;">
        <span style="color: white; font-size: 24px; font-weight: 500;"
          >User Info</span
        >
        <ul
          style="
            text-decoration: none;
            list-style: none;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            height: 80%;
          "
        >
          <li style="font-size: 16px; color: white;">{{ userInfo.address }}</li>
          <li style="font-size: 16px; color: white;">{{ userInfo.email }}</li>
          <li style="font-size: 16px; color: white;">{{ userInfo.phone }}</li>
        </ul>
      </div>
      <div style="font-size: 16px; color: white; display: flex; flex-direction: column; justify-content: center;">
        <!-- <span>
            {{ userInfo?.workHours[0] }}
        </span>
        <span style="margin-top: 16px;">
            {{ userInfo?.workHours[1] }}
        </span> -->
      </div>
    </footer>
  </div>
</template>

<style scoped></style>

<script>
import axios from "axios";

const BASEURL = "http://192.168.88.195:4004/api";

export default {
  name: "Header",
  data() {
    return {
      userInfo: Object,
    };
  },
  methods: {
    async getInfo() {
      try {
        const response = await axios.post(`${BASEURL}/site/getInfo`, {
          siteKey: "rabbit",
        });
        if (response.status === 200) {
          this.userInfo = response.data;
        } else {
          console.log("aldaa zaalaa bro");
        }
      } catch (error) {
        console.error("Error");
      }
    },
  },
  mounted() {
    this.getInfo();
  },
};
</script>
