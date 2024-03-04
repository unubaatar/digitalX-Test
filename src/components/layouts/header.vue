<template>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
  />
  <div>
    <header
      style="
        display: flex;
        background-color: blue;
        width: 100%;
        height: 72px;
        justify-content: space-between;
      "
    >
      <div style="margin: auto 8px; display: flex; align-items: center;">
        <img
          :src="userInfo.logoUrl"
          alt=""
          style="object-fit: contain; height: 56px; cursor: pointer"
        />
        <div style="margin-left: 16px; color: white; font-weight: 600; font-size: 24px">
        {{ userInfo.siteName }}
      </div>
      </div>
      <div style="display: flex; align-items: center">
        <span
          style="
            color: white;
            font-size: 24px;
            font-weight: 500;
            cursor: pointer;
            margin-right: 36px;
          "
          class="news"
          >News</span
        >
        <ul style="display: flex; justify-content: center; align-items: center">
          <li v-if="userInfo?.hasFacebook" ><a :href="userInfo.facebook" class="fa fa-facebook"></a></li>
          <li v-if="userInfo.hasInstagram"><a :href="userInfo.instagram" class="fa fa-twitter"></a></li>
          <li v-if="userInfo.hasTwitter"><a :href="userInfo.twitter" class="fa fa-instagram"></a></li>
        </ul>
      </div>
    </header>
  </div>
</template>


<script>
import axios from 'axios';

const BASEURL = "http://192.168.88.195:4004/api";

export default {
  name: "Header",
  data() {
    return {
      userInfo: Object
    };
  },
  methods: {
    async getInfo() {
      try {
        const response = await axios.post(`${BASEURL}/site/getInfo`, { siteKey: "rabbit" });
        if (response.status === 200) {
          this.userInfo = response.data;
        } else {
          console.log("aldaa zaalaa bro");
        }
      } catch (error) {
        console.error("Error");
      }
    }
  },
  mounted() {
    this.getInfo();
  }
};
</script>


<style scoped>
li {
  margin: 0px 16px;
  list-style: none;
}

.fa {
  font-size: 30px;
  width: 30px;
  text-align: center;
  text-decoration: none;
  padding: 8px;
}

.fa:hover {
  opacity: 0.7;
}

.fa-facebook {
  background: #3b5998;
  color: white;
  border-radius: 12px;
}

.fa-twitter {
  background: #55acee;
  color: white;
  border-radius: 12px;
}

.fa-instagram {
  background: #f40083;
  color: white;
  border-radius: 12px;
}

.news {
  padding: 8px;
  border-radius: 12px;
}

.news:hover {
  background-color: #3b5998;
}
</style>
