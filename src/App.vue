<template>
  <v-app>
    <router-view></router-view>
  </v-app>
</template>

<script>
// import axios from "axios"
import employee from "./mokup-data/employee.json";
import departments from "./mokup-data/departments.json";
import facilities from "./mokup-data/facilities.json";
import payment from "./mokup-data/payment.json";
import position from "./mokup-data/position.json";
import user from "./mokup-data/user.json";

export default {
  name: "App",
  mounted() {
    localStorage.setItem("employee", JSON.stringify(employee));
    localStorage.setItem("departments", JSON.stringify(departments));
    localStorage.setItem("facilities", JSON.stringify(facilities));
    localStorage.setItem("payment", JSON.stringify(payment));
    localStorage.setItem("payment", JSON.stringify(payment));
    localStorage.setItem("position", JSON.stringify(position));
    localStorage.setItem("user", JSON.stringify(user));
    const dataInfo = JSON.parse(localStorage.getItem("user-info"));
    if (dataInfo) {
      const dataUser = JSON.parse(localStorage.getItem("user"));
      const itemUser = dataUser.find((el) => el.email === dataInfo.email);
      dataInfo.password = itemUser.password;
      localStorage.setItem("user-info", JSON.stringify(dataInfo));
    }
  },
};
</script>
