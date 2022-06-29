<template>
  <div class="account">
    <v-container class="container">
      <v-row>
        <v-col cols="12">
          <!-- <h1>employee list</h1> -->
          <v-card>
            <v-card-title class="pb-0">
              DANH SÁCH TÀI KHOẢN
              <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Tìm Kiếm"
                single-line
                hide-details
              ></v-text-field>
            </v-card-title>
            <v-dialog v-model="dialog" max-width="600px">
              <template v-slot:activator="{ on, attrs }">
                <v-btn color="green" dark v-bind="attrs" v-on="on" class="ms-5 my-4">
                  Thêm Mới
                </v-btn>
              </template>
              <v-card>
                <v-card-title class="pt-7">
                  <span class="text-h5">{{ formTitle }}</span>
                </v-card-title>
                <v-card-text>
                  <v-container>
                    <v-row>
                      <v-col cols="12">
                        <v-text-field
                          label="Email*"
                          required
                          v-model="user.email"
                          :disabled="readChange"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <div class="input-container">
                          <v-text-field
                            label="Password*"
                            :type="choose"
                            required
                            v-model="user.password"
                          ></v-text-field>
                          <v-icon
                            class="material-icons visibility"
                            @click="showPassword"
                            >{{ visibility }}</v-icon
                          >
                        </div>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Họ"
                          required
                          v-model="user.lastName"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Tên"
                          required
                          v-model="user.firstName"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-select
                          :items="this.listRole"
                          label="Chức Vụ"
                          required
                          v-model="user.role"
                        ></v-select>
                      </v-col>
                    </v-row>
                  </v-container>
                  <small>*indicates required field</small>
                </v-card-text>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="blue darken-1" text @click="close">
                    Đóng
                  </v-btn>
                  <v-btn color="blue darken-1" text @click="createUser">
                    Cập nhật
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
            <v-data-table
              :headers="header"
              :items="account"
              :items-per-page="10"
              class="elevation-1 text-center table-list"
              item-key="id"
              show-select
              :search="search"
              :footer-props="{
                showFirstLastPage: true,
                firstIcon: 'mdi-arrow-collapse-left',
                lastIcon: 'mdi-arrow-collapse-right',
              }"
            >
              <template v-slot:[`item.actions`]="{ item }">
                <v-dialog max-width="600">
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      color="primary"
                      v-bind="attrs"
                      v-on="on"
                      @click="DetailsUser(item)"
                      >Chi Tiết <v-icon dark right> mdi-eye </v-icon>
                    </v-btn>
                  </template>
                  <template v-slot:default="dialogDetails">
                    <v-card class="pb-2">
                      <v-card-text class="pb-0">
                        <v-container class="px-0 pt-13 pb-0">
                          <h1 class="px-5 py-0 text-center primary--text">
                            Thông Tin Tài Khoản
                          </h1>
                          <v-row>
                            <v-col cols="12">
                              <v-text-field
                                label="ID"
                                required
                                :value="detailsItem.id"
                                readonly
                              ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                              <v-text-field
                                label="Email"
                                required
                                :value="detailsItem.email"
                                readonly
                              ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                              <div class="input-container">
                                <v-text-field
                                  label="Password"
                                  required
                                  :value="detailsItem.password"
                                  readonly
                                  :type="choose"
                                ></v-text-field>
                                <v-icon
                                  class="material-icons visibility"
                                  @click="showPassword"
                                  >{{ visibility }}</v-icon
                                >
                              </div>
                            </v-col>
                            <v-col cols="12">
                              <v-text-field
                                label="Tên nhân viên"
                                required
                                :value="
                                  detailsItem.lastName + ' ' + detailsItem.firstName
                                "
                                readonly
                              ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                              <v-text-field
                                label="Chức Vụ"
                                required
                                :value="detailsItem.role"
                                readonly
                              ></v-text-field>
                            </v-col>
                          </v-row>
                        </v-container>
                      </v-card-text>
                      <v-card-actions class="justify-end">
                        <v-btn
                          text
                          @click="dialogDetails.value = false"
                          color="primary"
                          >Đóng</v-btn
                        >
                      </v-card-actions>
                    </v-card>
                  </template>
                </v-dialog>
                <!-- <user-details
                  :id="detailsItem.id"
                  :email="detailsItem.email"
                  :password="detailsItem.password"
                  :role="detailsItem.role"
                  :timeLogin="detailsItem.timeLogin"
                  :detailsUser="DetailsUser(item)"
                ></user-details> -->
                <v-btn
                  class="ma-2"
                  color="orange darken-2"
                  dark
                  @click="editItem(item)"
                >
                  Sửa
                  <v-icon dark right> mdi-pencil </v-icon>
                </v-btn>
                <v-btn class="ma-2 ms-0" color="red" dark @click="handleRow(item)">
                  Xóa
                  <v-icon dark right> mdi-delete </v-icon>
                </v-btn>
              </template>
              <template v-slot:no-data>
                <v-btn color="primary"> Reset </v-btn>
              </template>
            </v-data-table>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
    <popup
      :show="showDialogDelete"
      :cancel="cancel"
      :confirm="handleDelete"
      text="Có! Mình muốn xóa ^^"
      title="Thông báo!"
      textCancel="Không nha :v"
      description="Bạn có muốn xóa dữ liệu này không ???"
    ></popup>
    <popup
      :show="showDialogUpdate"
      :cancel="cancel"
      :confirm="confirm"
      text="Oke ^^"
      title="Thông báo!"
      description="Sửa dữ liệu thành công!!"
    ></popup>
    <popup
      :show="showDialogCreateRequired"
      :cancel="cancel"
      :confirm="confirm"
      text="Ok! Mình sẽ kiểm tra lại"
      title="Thông báo!"
      description="Vui lòng điền đầy đủ thông tin!!"
    ></popup>
    <popup
      :show="showDialogCreateSuccess"
      :cancel="cancel"
      :confirm="confirm"
      text="Oke ^^"
      title="Thông báo!"
      description="Thêm dữ liệu thành công!!"
    ></popup>
    <popup
      :show="showDialogDeleteSuccess"
      :cancel="cancel"
      :confirm="confirm"
      text="Oke ^^"
      title="Thông báo!"
      description="Xoá dữ liệu thành công!!"
    ></popup>
    <popup
      :show="showDialogDuplicateEmail"
      :cancel="cancel"
      :confirm="confirm"
      text="Oke ^^"
      title="Thông báo!"
      description="Email này đã tồn tại!! Vui lòng chọn email khác"
    ></popup>
  </div>
</template>
<script>
// import axios from "axios";
import Popup from "../components/Popup.vue";
import { mapState } from "vuex";

export default {
  components: { Popup },
  data() {
    return {
      header: [
        {
          text: "ID",
          value: "id",
          align: "center",
        },
        {
          text: "Email",
          value: "email",
          align: "center",
        },
        {
          text: "Chức Vụ",
          value: "role",
          align: "center",
        },
        {
          text: "Thời Gian Đăng Nhập",
          value: "timeLogin",
          align: "center",
        },
        {
          text: "Chức Năng",
          value: "actions",
          align: "center",
          sortable: false,
        },
      ],
      user: {},
      defaultUser: {},
      deleteId: 0,
      detailsId: 0,
      account: [],
      search: "",
      dialog: false,
      dialogDetails: false,
      showDialogDelete: false,
      showDialogUpdate: false,
      showDialogCreateRequired: false,
      showDialogCreateSuccess: false,
      showDialogDeleteSuccess: false,
      showDialogDuplicateEmail: false,
      listRole: [],
      detailsItem: {},
      editedIndex: -1,
      readChange: false,
    };
  },
  methods: {
    async DetailsUser(item) {
      this.detailsId = item.id;
      const resData = JSON.parse(localStorage.getItem("user"));
      const details = [...resData].find((el) => el.id === this.detailsId);
      this.detailsItem = details;
    },
    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.user = Object.assign({}, this.defaultUser);
        this.editedIndex = -1;
        this.readChange = false;
      });
    },
    editItem(item) {
      this.dialog = true;
      this.editedIndex = this.account.indexOf(item);
      this.user = Object.assign({}, item);
      this.readChange = true;
      // console.log(this.user);
    },
    handleRow(item) {
      this.deleteId = item.email;
      this.showDialogDelete = true;
    },
    handleDelete() {
      const resDataUser = JSON.parse(localStorage.getItem("user"));
      const resDataEmp = JSON.parse(localStorage.getItem("employee"));
      const indexDel = resDataUser.findIndex((el) => el.email === this.deleteId);
      const index = resDataEmp.findIndex((el) => el.email === this.deleteId);
      resDataEmp.splice(index, 1);
      localStorage.setItem("employee", JSON.stringify(resDataEmp));
      resDataUser.splice(indexDel, 1);
      this.account = resDataUser;
      localStorage.setItem("user", JSON.stringify(resDataUser));
      this.showDialogDelete = false;
      this.showDialogDeleteSuccess = true;
    },
    cancel() {
      this.showDialogDelete = false;
      this.showDialogUpdate = false;
      this.showDialogCreateRequired = false;
      this.showDialogCreateSuccess = false;
      this.showDialogDeleteSuccess = false;
      this.showDialogDuplicateEmail = false;
    },
    confirm() {
      this.showDialogDelete = false;
      this.showDialogUpdate = false;
      this.showDialogCreateRequired = false;
      this.showDialogCreateSuccess = false;
      this.showDialogDeleteSuccess = false;
      this.showDialogDuplicateEmail = false;
    },
    showPassword() {
      this.$store.dispatch("actionSetShowPassword");
    },
    userExists(email) {
      const resUser = JSON.parse(localStorage.getItem("user"));
      return resUser.some(function(el) {
        return el.email === email;
      });
    },
    async createUser() {
      let today = new Date();
      if (this.editedIndex > -1) {
        if (this.user.email === "" || this.user.password === "") {
          this.showDialogCreateRequired = true;
          this.dialog = false;
        } else {
          let resDataEm = JSON.parse(localStorage.getItem("employee"));
          let resDataUser = JSON.parse(localStorage.getItem("user"));
          let resDataPay = JSON.parse(localStorage.getItem("payment"));
          const detailsUser = resDataUser[this.editedIndex];
          resDataUser.splice(this.editedIndex, 1, {
            id: detailsUser.id,
            email: this.user.email,
            password: this.user.password,
            firstName: this.user.firstName,
            lastName: this.user.lastName,
            role: this.user.role,
            timeLogin: detailsUser.timeLogin,
          });
          this.account = resDataUser;
          localStorage.setItem("user", JSON.stringify(resDataUser));
          const detailsEm = resDataEm[this.editedIndex];
          resDataEm.splice(this.editedIndex, 1, {
            id: detailsEm.id,
            emp_ID: detailsEm.emp_ID,
            firstName: this.user.firstName,
            lastName: this.user.lastName,
            email: this.user.email,
            password: this.user.password,
            imgUrl: detailsEm.imgUrl,
            role: this.user.role,
            depart_id: detailsEm.depart_id,
            depart_name: detailsEm.depart_name,
            position_id: detailsEm.position_id,
            address: detailsEm.address,
            phoneNumber: detailsEm.phoneNumber,
            birthday: detailsEm.birthday,
            gender: detailsEm.gender,
            numberCard: detailsEm.numberCard,
            nationality: detailsEm.nationality,
            ethnic: detailsEm.ethnic,
            religion: detailsEm.religion,
            educationalLevel: detailsEm.educationalLevel,
            academicLevel: detailsEm.academicLevel,
          });
          localStorage.setItem("employee", JSON.stringify(resDataEm));
          let detailsIndex = resDataPay.findIndex(
            (el) => el.emp_ID === detailsEm.emp_ID
          );
          const detailsPay = resDataPay.find((el) => el.emp_ID === detailsEm.emp_ID);
          if (detailsPay) {
            resDataPay.splice(detailsIndex, 1, {
              id: detailsPay.id,
              payment_ID: detailsPay.payment_ID,
              emp_ID: detailsPay.emp_ID,
              email: detailsPay.email,
              fullName: detailsPay.fullName,
              amount: detailsPay.amount,
              allowance: detailsPay.allowance,
              amount_total: Number(detailsPay.amount) + Number(detailsPay.allowance),
              role: this.user.role,
              description: detailsPay.description,
            });
            localStorage.setItem("payment", JSON.stringify(resDataPay));
          }

          this.showDialogUpdate = true;
          this.dialog = false;
        }
      } else {
        if (
          this.user.email == "" ||
          this.user.password == "" ||
          this.user.role == ""
        ) {
          this.showDialogCreateRequired = true;
          this.dialog = false;
        } else {
          if (this.userExists(this.user.email) == true) {
            this.showDialogDuplicateEmail = true;
            this.dialog = false;
          } else {
            const resUser = JSON.parse(localStorage.getItem("user"));
            const detailsIdUser = resUser[resUser.length - 1];
            resUser.push({
              id: detailsIdUser.id + 1,
              email: this.user.email,
              password: this.user.password,
              firstName: this.user.firstName,
              lastName: this.user.lastName,
              role: this.user.role,
              timeLogin: today.toLocaleString(),
            });
            this.account = resUser;
            localStorage.setItem("user", JSON.stringify(resUser));
            const resEm = JSON.parse(localStorage.getItem("employee"));
            const detailsIdEm = resEm[resEm.length - 1];
            resEm.push({
              id: detailsIdEm.id + 1,
              emp_ID: `NV${detailsIdEm.id + 1}`,
              firstName: this.user.firstName,
              lastName: this.user.lastName,
              email: this.user.email,
              password: this.user.password,
              role: this.user.role,
              position_id: this.user.position_id,
              depart_id: this.user.depart_id,
              depart_name: this.user.depart_name,
              address: this.user.address,
              imgUrl: this.user.imgUrl,
            });
            localStorage.setItem("employee", JSON.stringify(resEm));
            this.dialog = false;
            this.showDialogCreateSuccess = true;
          }
        }
      }
    },
  },
  async mounted() {
    const res = JSON.parse(localStorage.getItem("user"));
    this.account = res;
    const resPo = JSON.parse(localStorage.getItem("position"));
    let result = resPo.map((a) => a.role);
    this.listRole = result;
  },
  computed: {
    ...mapState({
      choose: (state) => state.choose,
      visibility: (state) => state.visibility,
    }),
    formTitle() {
      return this.editedIndex === -1 ? "Thêm mới tài khoản" : "Sửa tài khoản";
    },
  },
};
</script>
<style scoped>
h1 {
  text-transform: uppercase;
  text-align: center;
  margin: -10px 0 30px;
}
.input-container {
  position: relative;
}
.material-icons {
  margin: 0 10px;
  color: #aaa;
  cursor: default;
  position: absolute;
  content: "";
  top: 16px;
  right: -8px;
}
</style>
