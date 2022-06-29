<template>
  <div class="position">
    <v-container class="container">
      <v-row>
        <v-col cols="12">
          <!-- <h1>employee list</h1> -->
          <v-card>
            <v-card-title class="pb-0">
              DANH SÁCH CHỨC VỤ
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
                          label="Mã Chức Vụ"
                          required
                          v-model="positionItem.position_id"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Tên Chức Vụ"
                          required
                          v-model="positionItem.role"
                        ></v-text-field>
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
                  <v-btn color="blue darken-1" text @click="createPosition">
                    Cập nhật
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
            <v-data-table
              :headers="header"
              :items="position"
              :items-per-page="10"
              class="elevation-1 text-center"
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
                  <template v-slot:default="dialog">
                    <v-card class="pb-2">
                      <v-card-text class="pb-0">
                        <v-container class="px-0 pt-13 pb-0">
                          <h1 class="px-5 py-0 text-center primary--text">
                            Thông Tin Chức Vụ
                          </h1>
                          <v-row>
                            <v-col cols="12" sm="6">
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
                                    label="Mã Chức Vụ"
                                    required
                                    :value="detailsItem.position_id"
                                    readonly
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-text-field
                                    label="Tên Chức Vụ"
                                    required
                                    :value="detailsItem.role"
                                    readonly
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-text-field
                                    label="Số Lượng Nhân Sự"
                                    required
                                    :value="qtyPositon.length"
                                    readonly
                                  ></v-text-field>
                                </v-col>
                              </v-row>
                            </v-col>
                            <v-col cols="12" sm="6">
                              <v-row>
                                <v-col cols="12">
                                  <v-text-field
                                    label="Người Tạo"
                                    required
                                    readonly
                                    v-model="detailsItem.user_create"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-text-field
                                    label="Ngày Tạo"
                                    required
                                    readonly
                                    v-model="detailsItem.time_create"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-text-field
                                    label="Người Sửa"
                                    required
                                    readonly
                                    v-model="detailsItem.user_update"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-text-field
                                    label="Ngày Sửa"
                                    required
                                    readonly
                                    v-model="detailsItem.time_update"
                                  ></v-text-field>
                                </v-col>
                              </v-row>
                            </v-col>
                          </v-row>
                        </v-container>
                      </v-card-text>
                      <v-card-actions class="justify-end">
                        <v-btn text @click="dialog.value = false" color="primary"
                          >Đóng</v-btn
                        >
                      </v-card-actions>
                    </v-card>
                  </template>
                </v-dialog>
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
      :show="showDialogDeleteSuccess"
      :cancel="cancel"
      :confirm="confirm"
      text="Oke ^^"
      title="Thông báo!"
      description="Xoá dữ liệu thành công!!"
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
      :show="showDialogUpdate"
      :cancel="cancel"
      :confirm="confirm"
      text="Oke ^^"
      title="Thông báo!"
      description="Sửa dữ liệu thành công!!"
    ></popup>
  </div>
</template>
<script>
// import axios from "axios";
import Popup from "../components/Popup.vue";
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
          text: "Mã Chức Vụ",
          value: "position_id",
          align: "center",
        },
        {
          text: "Tên Chức Vụ",
          value: "role",
          align: "center",
        },
        {
          text: "Người Tạo",
          value: "user_create",
          align: "center",
        },
        {
          text: "Ngày Tạo",
          value: "time_create",
          align: "center",
        },
        {
          text: "Người Sửa",
          value: "user_update",
          align: "center",
        },
        {
          text: "Ngày Sửa",
          value: "time_update",
          align: "center",
        },
        {
          text: "Chức Năng",
          value: "actions",
          align: "center",
          sortable: false,
        },
      ],
      position: [],
      search: "",
      detailsItem: {},
      detailsId: 0,
      deleteId: 0,
      dialog: false,
      positionItem: {},
      positionItemDefault: {},
      showDialogDelete: false,
      showDialogDeleteSuccess: false,
      showDialogCreateRequired: false,
      showDialogCreateSuccess: false,
      showDialogUpdate: false,
      qtyPositon: [],
      editedIndex: -1,
    };
  },
  async mounted() {
    const res = JSON.parse(localStorage.getItem("position"));
    this.position = res;
  },
  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "Thêm mới chức vụ" : "Sửa thông tin chức vụ";
    },
    inputTitleUser() {
      return this.editedIndex === -1 ? "Người Tạo" : "Người Sửa";
    },
    inputTitleDay() {
      return this.editedIndex === -1 ? "Ngày Tạo" : "Ngày Sửa";
    },
  },
  methods: {
    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.positionItem = Object.assign({}, this.positionItemDefault);
        this.editedIndex = -1;
      });
    },
    editItem(item) {
      this.dialog = true;
      this.editedIndex = this.position.indexOf(item);
      this.positionItem = Object.assign({}, item);
      // console.log(this.user);
    },
    async createPosition() {
      const resInfo = JSON.parse(localStorage.getItem("user-info"));
      let today = new Date();
      if (this.editedIndex > -1) {
        let result = Object.values(this.positionItem);
        let resultRequired = result.find((el) => el === "");
        if (resultRequired != undefined) {
          this.showDialogCreateRequired = true;
          this.dialog = false;
        } else {
          let resDataPo = JSON.parse(localStorage.getItem("position"));
          const detailsPo = resDataPo[this.editedIndex];
          resDataPo.splice(this.editedIndex, 1, {
            id: detailsPo.id,
            position_id: this.positionItem.position_id,
            role: this.positionItem.role,
            user_create: this.positionItem.user_create,
            time_create: this.positionItem.time_create,
            user_update: resInfo.role,
            time_update: today.toLocaleString(),
          });
          this.position = resDataPo;
          localStorage.setItem("position", JSON.stringify(resDataPo));
          this.showDialogUpdate = true;
          this.dialog = false;
        }
      } else {
        if (this.positionItem.position_id == "" || this.positionItem.role == "") {
          this.showDialogCreateRequired = true;
          this.dialog = false;
        } else {
          const resPo = JSON.parse(localStorage.getItem("position"));
          const detailsIdDe = resPo[resPo.length - 1];
          resPo.push({
            id: detailsIdDe.id + 1,
            position_id: this.positionItem.position_id,
            role: this.positionItem.role,
            user_create: resInfo.role,
            time_create: today.toLocaleString(),
            user_update: this.positionItem.user_update,
            time_update: this.positionItem.time_update,
          });
          this.position = resPo;
          localStorage.setItem("position", JSON.stringify(resPo));
          this.dialog = false;
          this.showDialogCreateSuccess = true;
        }
      }
    },
    async DetailsUser(item) {
      this.detailsId = item.id;
      const resData = JSON.parse(localStorage.getItem("position"));
      const details = [...resData].find((el) => el.id === this.detailsId);
      this.detailsItem = details;
      const dataEm = JSON.parse(localStorage.getItem("employee"));
      const detailsQty = dataEm.filter((el) => el.role === this.detailsItem.role);
      this.qtyPositon = detailsQty;
    },
    handleRow(item) {
      this.deleteId = item.id;
      this.showDialogDelete = true;
    },
    async handleDelete() {
      const resDataPo = JSON.parse(localStorage.getItem("position"));
      const indexDel = resDataPo.findIndex((el) => el.id === this.deleteId);
      resDataPo.splice(indexDel, 1);
      this.position = resDataPo;
      localStorage.setItem("position", JSON.stringify(resDataPo));
      this.showDialogDelete = false;
      this.showDialogDeleteSuccess = true;
    },
    cancel() {
      this.showDialogDelete = false;
      this.showDialogDeleteSuccess = false;
      this.showDialogCreateRequired = false;
      this.showDialogCreateSuccess = false;
      this.showDialogUpdate = false;
    },
    confirm() {
      this.showDialogDelete = false;
      this.showDialogDeleteSuccess = false;
      this.showDialogCreateRequired = false;
      this.showDialogCreateSuccess = false;
      this.showDialogUpdate = false;
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
</style>
