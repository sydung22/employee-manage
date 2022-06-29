<template>
  <div>
    <v-navigation-drawer v-if="!drawer" app>
      <v-img
        height="140"
        class="pa-4"
        src="https://bigdata-vn.com/wp-content/uploads/2021/09/Background-anh-sang-dep.jpg"
      >
        <div class="text-center">
          <v-avatar class="mb-2" color="grey darken-1" size="78" v-if="imgUrl">
            <v-img aspect-ratio="30" :src="imgUrl" />
          </v-avatar>
          <v-avatar class="mb-2" color="grey darken-1" size="78" v-else>
            <v-img
              aspect-ratio="30"
              src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTv_8jyrBjic0ELBWNbA2JH7ufzOb3jkJvN8Q&usqp=CAU"
            />
          </v-avatar>
          <h3 class="white--text" v-if="lastName && firstName">
            {{ lastName }} {{ firstName }}
          </h3>
          <h3 class="white--text" v-else>Người dùng mới</h3>
        </div>
      </v-img>
      <!-- <v-divider></v-divider> -->
      <v-list class="red_list">
        <v-list-item-group>
          <v-list-item
            v-for="(link, i) in links"
            :key="i"
            link
            @click="positionAction(link.action)"
            class="item-sidebar ps-5"
          >
            <v-list-item-icon>
              <v-icon>{{ link.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content style="color: #ADB3B3">
              {{ link.title }}
            </v-list-item-content>
          </v-list-item>
          <div class="text-center">
            <v-menu :offset-x="offset">
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  color="#ADB3B3"
                  text
                  class="button-sidebar"
                  height="56px"
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon
                    dark
                    right
                    class="me-8 icon-sidebar"
                    style="font-size: 24px;"
                  >
                    mdi-inbox-multiple</v-icon
                  >

                  Danh Sách Khác
                </v-btn>
              </template>

              <v-list max-width="100%" class="listitem-sidebar">
                <v-list-item
                  v-for="(item, index) in items"
                  :key="index"
                  @click="positionAction(item.action)"
                  style=" color: #ADB3B3"
                >
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
          </div>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
    <popup
      :show="showDialogRole"
      :cancel="cancel"
      :confirm="confirm"
      text="Oke ^^"
      title="Thông báo!"
      description="Bạn không có quyền hạn vào đây!! Xin cảm ơn"
    ></popup>
  </div>
</template>

<script>
import Popup from "./Popup.vue";
// import { mapState } from "vuex";
// import axios from "axios";
export default {
  components: { Popup },
  name: "Sidebar",
  props: ["drawer"],
  data() {
    return {
      links: [
        {
          icon: "mdi-microsoft-windows",
          title: "Trang Chủ",
          action: "dashboard",
        },
        {
          icon: "mdi-card-account-details-outline",
          title: "Tài Khoản",
          action: "user",
        },
        {
          icon: "mdi-account-multiple",
          title: "Nhân Viên",
          action: "employee",
        },
        {
          icon: "mdi-desktop-classic",
          title: "Cơ Sở Vật Chất",
          action: "facilities",
        },
        // {
        //   icon: "mdi-home-city",
        //   title: "Phòng Ban",
        //   action: "department",
        // },
        // {
        //   icon: "mdi-shield-account",
        //   title: "Chức Vụ",
        //   action: "position",
        // },
        {
          icon: "mdi-cash-multiple",
          title: "Tiền Lương",
          action: "payment",
        },
        {
          icon: "mdi-file-sign",
          title: "Báo Cáo",
          action: "report",
        },
        {
          icon: "mdi-newspaper-variant-outline",
          title: "Tin Tức",
          action: "news",
        },
        {
          icon: "mdi-ballot-outline",
          title: "Thủ Tục",
          action: "procedure",
        },
        {
          icon: "mdi-cog",
          title: "Tiện Ích",
          action: "settings",
        },
      ],
      firstName: "",
      lastName: "",
      imgUrl: "",
      role: "",
      department: "",
      model: 0,
      showDialogRole: false,
      items: [
        { title: "Danh sách tài khoản", action: "user" },
        { title: "Danh sách phòng ban", action: "department" },
        { title: "Danh sách chức vụ", action: "position" },
        { title: "Thống kê doanh thu", action: "report" },
      ],
      offset: true,
    };
  },
  async mounted() {
    // const res = await axios.get(`${process.env.VUE_APP_SERVER_URL}/employee`);
    const res = JSON.parse(localStorage.getItem("employee"));
    const dataLogin = JSON.parse(localStorage.getItem("user-info"));
    let email = dataLogin.email;
    let data = res;
    const index = data.find((el) => el.email === email);
    //  const index =  data.map(el => el.email == id)
    this.firstName = index.firstName;
    this.lastName = index.lastName;
    this.imgUrl = index.imgUrl;
    this.role = index.role;
    this.department = index.depart_name;

    if (this.$route.name === "user") {
      if (
        this.role === "Admin" ||
        this.role === "Trưởng Phòng" ||
        this.role === "Giám Đốc Công Ty"
      ) {
        if (this.$route.name === "user") return;
        this.$router.push("/user");
      } else {
        this.$router.push("/");
        setTimeout(() => alert("Bạn không có quyền hạn để vào"), 400);
      }
    }
    if (this.$route.name === "employee") {
      if (
        this.role === "Admin" ||
        this.role === "Trưởng Phòng" ||
        this.role === "Giám Đốc CSVC" ||
        this.role === "Giám Đốc Công Ty"
      ) {
        if (this.$route.name === "employee") return;
        this.$router.push("/employee");
      } else {
        this.$router.push("/");
        setTimeout(() => alert("Bạn không có quyền hạn để vào"), 400);
      }
      console.log("this is", this.$route.name);
    }
    if (this.$route.name === "facilities") {
      if (
        this.role === "Admin" ||
        this.role === "Nhân Viên" ||
        this.role === "Giám Đốc CSVC" ||
        this.role === "Giám Đốc Công Ty" ||
        (this.role === "Trưởng Phòng" && this.department === "Phòng Cơ Sở Vật Chất")
      ) {
        if (this.$route.name === "facilities") return;
        this.$router.push("/facilities");
      } else {
        this.$router.push("/");
        setTimeout(() => alert("Bạn không có quyền hạn để vào"), 400);
      }
    }
    if (this.$route.name === "department") {
      if (
        this.role === "Admin" ||
        this.role === "Trưởng Phòng" ||
        this.role === "Giám Đốc Công Ty"
      ) {
        if (this.$route.name === "department") return;
        this.$router.push("/department");
      } else {
        this.$router.push("/");
        setTimeout(() => alert("Bạn không có quyền hạn để vào"), 400);
      }
    }
    if (this.$route.name === "position") {
      if (
        this.role === "Admin" ||
        this.role === "Trưởng Phòng" ||
        this.role === "Giám Đốc Công Ty"
      ) {
        if (this.$route.name === "position") return;
        this.$router.push("/position");
      } else {
        this.$router.push("/");
        setTimeout(() => alert("Bạn không có quyền hạn để vào"), 400);
      }
    }
    if (this.$route.name === "payment") {
      if (
        this.role === "Admin" ||
        this.role === "Trưởng Phòng" ||
        this.role === "Nhân Viên" ||
        this.role === "Giám Đốc Công Ty"
      ) {
        if (this.$route.name === "payment") return;
        this.$router.push("/payment");
      } else {
        this.$router.push("/");
        setTimeout(() => alert("Bạn không có quyền hạn để vào"), 400);
      }
    }
  },
  methods: {
    confirm() {
      this.showDialogRole = false;
    },
    cancel() {
      console.log("thành công");
    },
    positionAction(action) {
      switch (action) {
        case "dashboard":
          if (this.$route.name !== "dashboard") {
            this.$router.push("/");
          } else {
            return;
          }
          break;
        case "user":
          if (this.$route.name !== "user") {
            if (
              this.role === "Admin" ||
              this.role === "Trưởng Phòng" ||
              this.role === "Giám Đốc Công Ty"
            ) {
              this.$router.push("/user");
              console.log(this.$route.name);
            } else {
              this.showDialogRole = true;
            }
          } else {
            return;
          }
          break;
        case "employee":
          if (this.$route.name !== "employee") {
            if (
              this.role === "Admin" ||
              this.role === "Trưởng Phòng" ||
              this.role === "Giám Đốc CSVC" ||
              this.role === "Giám Đốc Công Ty"
            ) {
              this.$router.push("/employee");
            } else {
              this.showDialogRole = true;
            }
          } else {
            return;
          }

          break;
        case "facilities":
          if (this.$route.name !== "facilities") {
            if (
              this.role === "Admin" ||
              this.role === "Nhân Viên" ||
              this.role === "Giám Đốc CSVC" ||
              (this.role === "Trưởng Phòng" &&
                this.department === "Phòng Cơ Sở Vật Chất") ||
              this.role === "Giám Đốc Công Ty"
            ) {
              this.$router.push("/facilities");
            } else {
              this.showDialogRole = true;
            }
          } else {
            return;
          }
          break;
        case "department":
          if (this.$route.name !== "department") {
            if (
              this.role === "Admin" ||
              this.role === "Trưởng Phòng" ||
              this.role === "Giám Đốc Công Ty"
            ) {
              this.$router.push("/department");
            } else {
              this.showDialogRole = true;
            }
          } else {
            return;
          }
          break;
        case "position":
          if (this.$route.name !== "position") {
            if (
              this.role === "Admin" ||
              this.role === "Trưởng Phòng" ||
              this.role === "Giám Đốc Công Ty"
            ) {
              this.$router.push("/position");
            } else {
              this.showDialogRole = true;
            }
          } else {
            return;
          }

          break;
        case "payment":
          if (this.$route.name !== "payment") {
            if (
              this.role === "Admin" ||
              this.role === "Trưởng Phòng" ||
              this.role === "Nhân Viên" ||
              this.role === "Giám Đốc Công Ty"
            ) {
              this.$router.push("/payment");
            } else {
              this.showDialogRole = true;
            }
          } else {
            return;
          }
          break;

        case "report":
          if (this.$route.name !== "report") {
            if (this.role === "Admin" || this.role === "Giám Đốc Công Ty") {
              this.$router.push("/report");
            } else {
              this.showDialogRole = true;
            }
          } else {
            return;
          }

          break;
        default:
          this.$router.push("/pageupdate");
      }
    },
  },
  //     computed: {
  //   ...mapState({
  //     userInfo: (state) => state.userInfo,
  //     imageInfo: (state) => state.imageInfo,
  //   }),
  // },
};
</script>

<style scoped>
a {
  text-decoration: none;
  color: green !important;
  display: block;
}
a,
i {
  color: #adb3b3 !important;
  transition: 0.2s;
}
.v-list-item--link,
.v-list-item__content {
  transition: 0.2s;
}
.v-list-item--link:hover,
.button-sidebar:hover {
  background: linear-gradient(
    90deg,
    rgba(4, 161, 46, 1) 10%,
    rgba(0, 0, 0, 0.7147233893557423) 80%
  );
  color: #fff !important;
}
.button-sidebar:hover .icon-sidebar {
  color: #fff !important;
}
.button-sidebar {
  border-radius: unset;
  transition: 0.2s;
  display: block;
  width: 100%;
  text-align: left;
  align-items: flex-start;
  justify-content: flex-start;
  text-transform: unset;
  font-size: 16px !important;
  font-weight: normal;
  letter-spacing: 0;
}
.bg-list {
  background: url("https://cdn.pixabay.com/photo/2017/05/11/08/37/universe-2303321_960_720.jpg")
    no-repeat center 0px !important;
  background-size: cover;
}
/* .theme--light.v-list-item--active .v-list-item__content,
.theme--light.v-list-item--active i, */
.v-list-item--link:hover .v-list-item__content,
.v-list-item--link:hover i,
.red_list .v-list-item-group .v-list-item--active .v-list-item__content,
.red_list .v-list-item-group .v-list-item--active i {
  color: #fff !important;
}
.item-sidebar {
  display: flex;
}
/* .theme--light.v-list-item--active:hover::before,
.theme--light.v-list-item--active::before {
  opacity: 1;
}
.v-list-item--link:before {
  z-index: -1;
  background-color: green;
} */
.theme--light.v-navigation-drawer {
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.65), rgba(0, 0, 0, 0.65)),
    url("https://cdn.pixabay.com/photo/2017/05/11/08/37/universe-2303321_960_720.jpg")
      center 0px !important;
  background-size: cover;
  width: 260px !important;
}
.red_list .v-list-item-group .v-list-item--active,
.listitem-sidebar .v-list-item--active {
  background: linear-gradient(
    90deg,
    rgba(4, 161, 46, 1) 10%,
    rgba(0, 0, 0, 0.7147233893557423) 80%
  );
  color: #fff !important;
}
.listitem-sidebar .v-list-item--active::before {
  opacity: 0;
}
.button-sidebar::before {
  background: unset !important;
}
.listitem-sidebar {
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.65), rgba(0, 0, 0, 0.65)),
    url("https://img2.thuthuat123.com/uploads/2019/11/19/anh-background-ban-dem-rat-dep_122620804.jpg") !important;
  background-size: cover !important;
  background-position: center !important;
}
.theme--light.v-list-item:hover::before {
  opacity: 0 !important;
}
</style>
