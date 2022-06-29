<template>
  <div class="employee">
    <v-container class="container">
      <v-row>
        <v-col cols="12">
          <!-- <h1>employee list</h1> -->
          <v-card>
            <v-card-title class="pb-0">
              DANH SÁCH NHÂN VIÊN
              <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Tìm Kiếm"
                single-line
                hide-details
              ></v-text-field>
            </v-card-title>
            <v-dialog v-model="dialog" max-width="1200px">
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
                      <v-col cols="12" sm="6" class="text-center">
                        <v-container>
                          <v-row>
                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                :counter="30"
                                label="Họ"
                                v-model="user.lastName"
                                required
                              ></v-text-field>
                            </v-col>
                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                :counter="30"
                                label="Tên"
                                v-model="user.firstName"
                                required
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="E-mail"
                                v-model="user.email"
                                required
                                :disabled="readChange"
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Link Hình Ảnh"
                                v-model="user.imgUrl"
                                required
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Địa Chỉ"
                                v-model="user.address"
                                required
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-select
                                :items="this.listRole"
                                label="Chức Vụ"
                                v-model="user.role"
                                required
                              ></v-select>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-select
                                :items="this.listDepartment"
                                label="Phòng Ban"
                                v-model="user.depart_name"
                                required
                              ></v-select>
                            </v-col>
                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-select
                                :items="maritalList"
                                label="Tình Trạng Hôn Nhân"
                                v-model="user.marital_status"
                                required
                              ></v-select>
                            </v-col>
                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Số Điện Thoại"
                                v-model="user.phoneNumber"
                                required
                                class="pt-1"
                              ></v-text-field>
                            </v-col>
                          </v-row>
                        </v-container>
                      </v-col>
                      <v-col cols="12" sm="6" class="text-center">
                        <v-container>
                          <v-row>
                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Ngày Sinh"
                                v-model="user.birthday"
                                required
                                type="date"
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-select
                                :items="['Nam', 'Nữ']"
                                label="Giới Tính"
                                v-model="user.gender"
                                required
                              ></v-select>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Số CMND/CCCD"
                                v-model="user.numberCard"
                                required
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Quốc Tịch"
                                v-model="user.nationality"
                                required
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Dân Tộc"
                                v-model="user.ethnic"
                                required
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Tôn Giáo"
                                v-model="user.religion"
                                required
                              ></v-text-field>
                            </v-col>

                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-select
                                :items="educationList"
                                label="Trình Độ"
                                required
                                v-model="user.educationalLevel"
                              ></v-select>
                            </v-col>
                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-text-field
                                label="Bằng Cấp"
                                v-model="user.degree"
                                required
                              ></v-text-field>
                            </v-col>
                            <v-col cols="12" md="12" class="pb-0 pt-1">
                              <v-select
                                class="pt-1"
                                :items="academicList"
                                label="Chuyên Môn"
                                :menu-props="{ top: true, offsetY: true }"
                                required
                                v-model="user.academicLevel"
                              ></v-select>
                            </v-col>
                          </v-row>
                        </v-container>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card-text>
                <v-card-actions class="pt-0 pb-4">
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
              :items="employee"
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
              <template v-slot:[`item.imgUrl`]="{ item }">
                <img
                  v-if="item.imgUrl"
                  :src="item.imgUrl"
                  style="width: 60px; height: 50px; object-fit:cover; margin: 3px 0 -2px"
                />
                <img
                  v-else
                  src="https://timbee.com.vn/Data/Sites/2/News/2184/user.png"
                  style="width: 60px; height: 50px; object-fit:cover; margin: 3px 0 -2px;"
                />
              </template>
              <template v-slot:[`item.actions`]="{ item }">
                <v-dialog max-width="1600">
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
                    <v-card class="pb-3">
                      <v-card-text class="pb-4">
                        <v-container class="px-0 pt-13 pb-0">
                          <h1 class="px-5 py-0 text-center primary--text">
                            Thông Tin Nhân Viên
                          </h1>
                          <v-row align="center" justify="center" class="pe-5">
                            <v-col cols="12" sm="3" class="text-center">
                              <v-avatar
                                class="mb-2"
                                color="grey darken-1"
                                size="300"
                                v-if="detailsItem.imgUrl"
                              >
                                <v-img aspect-ratio="30" :src="detailsItem.imgUrl" />
                              </v-avatar>
                              <v-avatar
                                class="mb-2"
                                color="grey darken-1"
                                size="250"
                                v-else
                              >
                                <v-img
                                  aspect-ratio="30"
                                  src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTv_8jyrBjic0ELBWNbA2JH7ufzOb3jkJvN8Q&usqp=CAU"
                                />
                              </v-avatar>
                              <h2
                                class="black--text mt-2 mb-6"
                                v-if="detailsItem.firstName && detailsItem.lastName"
                              >
                                {{ detailsItem.lastName }}
                                {{ detailsItem.firstName }}
                              </h2>
                              <h2 class="black--text mt-2 mb-6" v-else>
                                Người dùng mới
                              </h2>
                              <v-row
                                align="center"
                                justify="center"
                                v-for="(link, index) in linkUser"
                                :key="index"
                                class="mt-0 ms-5"
                              >
                                <v-col cols="12" sm="2" class="text-end px-0 mb-2">
                                  <v-avatar
                                    class="mb"
                                    color="grey darken-1"
                                    size="30"
                                  >
                                    <v-img aspect-ratio="30" :src="link.imgUrl" />
                                  </v-avatar>
                                </v-col>
                                <v-col cols="12" sm="10" class="text-start">
                                  <h4 class="primary--text">
                                    {{ link.titleUrl }}
                                  </h4>
                                </v-col>
                              </v-row>
                            </v-col>
                            <v-col cols="12" sm="3" class="text-center">
                              <v-form>
                                <v-container>
                                  <v-row>
                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="ID"
                                        :value="detailsItem.id"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Mã Nhân Viên"
                                        :value="detailsItem.emp_ID"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>
                                    <v-col
                                      cols="12"
                                      md="12"
                                      class="pb-0 pt-1"
                                      v-if="
                                        detailsItem.lastName && detailsItem.firstName
                                      "
                                    >
                                      <v-text-field
                                        label="Tên Nhân Viên"
                                        :value="
                                          detailsItem.lastName +
                                            ' ' +
                                            detailsItem.firstName
                                        "
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>
                                    <v-col
                                      cols="12"
                                      md="12"
                                      class="pb-0 pt-1"
                                      v-else
                                    >
                                      <v-text-field
                                        label="Tên Nhân Viên"
                                        value="Người dùng mới"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="E-mail"
                                        :value="detailsItem.email"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Số điện thoại"
                                        :value="detailsItem.phoneNumber"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Địa Chỉ"
                                        :value="detailsItem.address"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Chức Vụ"
                                        :value="detailsItem.role"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Phòng Ban"
                                        :value="detailsItem.depart_name"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Tình Trạng Hôn Nhân"
                                        :value="detailsItem.marital_status"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>
                                  </v-row>
                                </v-container>
                              </v-form>
                            </v-col>
                            <v-col cols="12" sm="3" class="text-center">
                              <v-form>
                                <v-container>
                                  <v-row>
                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Ngày Sinh"
                                        :value="detailsItem.birthday"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-select
                                        :items="['Nam', 'Nữ']"
                                        label="Giới Tính"
                                        :value="detailsItem.gender"
                                        required
                                        readonly
                                      ></v-select>
                                    </v-col>
                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Số CMND/CCCD"
                                        :value="detailsItem.numberCard"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Quốc Tịch"
                                        :value="detailsItem.nationality"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Dân Tộc"
                                        :value="detailsItem.ethnic"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Tôn Giáo"
                                        :value="detailsItem.religion"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-select
                                        :items="educationList"
                                        label="Trình Độ"
                                        :value="detailsItem.educationalLevel"
                                        required
                                        readonly
                                      ></v-select>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-text-field
                                        label="Bằng Cấp"
                                        :value="detailsItem.degree"
                                        required
                                        readonly
                                      ></v-text-field>
                                    </v-col>

                                    <v-col cols="12" md="12" class="pb-0 pt-1">
                                      <v-select
                                        :items="academicList"
                                        label="Chuyên Môn"
                                        :value="detailsItem.academicLevel"
                                        :menu-props="{
                                          top: true,
                                          offsetY: true,
                                        }"
                                        required
                                        readonly
                                      ></v-select>
                                    </v-col>
                                  </v-row>
                                </v-container>
                              </v-form>
                            </v-col>
                            <v-col cols="12" sm="3" class="text-center">
                              <v-card class="mx-auto" max-width="400">
                                <v-img
                                  class="white--text align-end"
                                  height="200px"
                                  src="https://www.constructionplusasia.com/wp-content/uploads/2020/05/1-03.jpg"
                                >
                                </v-img>

                                <v-card-subtitle
                                  class="pb-2 pt-3"
                                  style="font-size: 16px"
                                >
                                  Công Ty Axon Active
                                </v-card-subtitle>

                                <v-card-text class="text--primary">
                                  <div>Nhân viên lập trình VueJS</div>
                                  <div>Thời gian làm việc: 2 năm</div>
                                </v-card-text>
                              </v-card>
                              <v-card class="mx-auto mt-5" max-width="400">
                                <v-img
                                  class="white--text align-end"
                                  height="200px"
                                  src="https://i.pinimg.com/originals/fa/dd/01/fadd011335400a0262227ed6f250b313.jpg"
                                >
                                </v-img>
                                <v-card-subtitle
                                  class="pb-2 pt-3"
                                  style="font-size: 16px"
                                >
                                  Công Ty Paradox Software
                                </v-card-subtitle>
                                <v-card-text class="text--primary">
                                  <div>Nhân viên lập trình NodeJS</div>
                                  <div>Thời gian làm việc: 2.5 năm</div>
                                </v-card-text>
                              </v-card>
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
      :show="showDialogDuplicateEmail"
      :cancel="cancel"
      :confirm="confirm"
      text="Oke ^^"
      title="Thông báo!"
      description="Email này đã tồn tại!! Vui lòng chọn email khác"
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
          text: "Họ",
          value: "lastName",
          align: "center",
        },
        {
          text: "Tên",
          value: "firstName",
          align: "center",
        },
        {
          text: "Hình Ảnh",
          value: "imgUrl",
          align: "center",
        },
        {
          text: "Chức Vụ",
          value: "role",
          align: "center",
        },
        {
          text: "Phòng Ban",
          value: "depart_name",
          align: "center",
        },
        {
          text: "Địa Chỉ",
          value: "address",
          align: "center",
        },
        {
          text: "Chức Năng",
          value: "actions",
          align: "center",
          sortable: false,
        },
      ],
      employee: [],
      listRole: [],
      listDepartment: [],
      search: "",
      deleteId: 0,
      detailsId: 0,
      dialog: false,
      detailsItem: {},
      user: {
        ethnic: "Kinh",
        nationality: "Việt Nam",
        religion: "Không có",
      },
      defaultUser: {
        ethnic: "Kinh",
        nationality: "Việt Nam",
        religion: "Không có",
      },
      showDialogDelete: false,
      showDialogDeleteSuccess: false,
      showDialogCreateRequired: false,
      showDialogCreateSuccess: false,
      showDialogDuplicateEmail: false,
      showDialogUpdate: false,
      linkUser: [
        {
          imgUrl:
            "https://br.atsit.in/vi/wp-content/uploads/2021/06/anh-facebook-khong-tai-hoac-khong-hien-thi-loi-khong-the-ket-noi-bat-len-ban-khong-don-doc.png",
          titleUrl: "https://www.facebook.com/",
        },
        {
          imgUrl:
            "https://is1-ssl.mzstatic.com/image/thumb/Purple118/v4/90/96/fc/9096fc60-7d7f-b8a1-f152-882c02811ddc/AppIcon_v3-85-220-4-2x.png/1200x630bb.png",
          titleUrl: "https://www.google.com/intl/vi/gmail/about/",
        },
        {
          imgUrl:
            "https://cdn.pixabay.com/photo/2017/08/05/11/24/logo-2582757__480.png",
          titleUrl: "https://github.com/",
        },
        {
          imgUrl:
            "https://image.similarpng.com/very-thumbnail/2020/05/Glossy-Instagram-icon-PNG.png",
          titleUrl: "https://www.instagram.com/",
        },
      ],
      educationList: [
        "9/12",
        "10/12",
        "11/12",
        "12/12",
        "Cao Đẳng",
        "Đại Học",
        "Cử Nhân",
        "Thạc Sĩ",
        "Tiến Sĩ",
      ],
      academicList: [
        "Không",
        "Bán Lẻ",
        "Kinh Doanh",
        "Vận Tải & Hậu Cần",
        "Quản Lý Nhân Lực",
        "Khởi Nghiệp",
        "Marketing",
        "Công Nghệ Thông Tin",
        "Kiểm Toán",
        "Chăm Sóc Khách Hàng",
        "Kế Toán",
      ],
      maritalList: ["Độc Thân", "Đã Có Gia Đình", "Ly Thân"],
      editedIndex: -1,
      readChange: false,
    };
  },
  methods: {
    DetailsUser(item) {
      this.detailsId = item.id;
      const resData = JSON.parse(localStorage.getItem("employee"));
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
      this.editedIndex = this.employee.indexOf(item);
      this.user = Object.assign({}, item);
      this.readChange = true;
      // console.log(this.user);
    },
    handleRow(item) {
      this.deleteId = item.email;
      this.showDialogDelete = true;
    },
    async handleDelete() {
      const resDataUser = JSON.parse(localStorage.getItem("user"));
      const resDataEmp = JSON.parse(localStorage.getItem("employee"));
      const indexDel = resDataUser.findIndex((el) => el.email === this.deleteId);
      const index = resDataEmp.findIndex((el) => el.email === this.deleteId);
      resDataEmp.splice(index, 1);
      localStorage.setItem("employee", JSON.stringify(resDataEmp));
      resDataUser.splice(indexDel, 1);
      this.employee = resDataEmp;
      localStorage.setItem("user", JSON.stringify(resDataUser));
      this.showDialogDelete = false;
      this.showDialogDeleteSuccess = true;
    },
    userExists(email) {
      const resUser = JSON.parse(localStorage.getItem("employee"));
      return resUser.some(function(el) {
        return el.email === email;
      });
    },
    async createUser() {
      let today = new Date();
      if (this.editedIndex > -1) {
        let result = Object.values(this.user);
        let resultRequired = result.find((el) => el === "");
        if (resultRequired != undefined) {
          this.showDialogCreateRequired = true;
          this.dialog = false;
        } else {
          let resDataEm = JSON.parse(localStorage.getItem("employee"));
          let resDataUser = JSON.parse(localStorage.getItem("user"));
          let resDataPay = JSON.parse(localStorage.getItem("payment"));
          //Employee
          const detailsEm = resDataEm[this.editedIndex];
          resDataEm.splice(this.editedIndex, 1, {
            id: detailsEm.id,
            emp_ID: detailsEm.emp_ID,
            firstName: this.user.firstName,
            lastName: this.user.lastName,
            email: this.user.email,
            password: this.user.password,
            imgUrl: this.user.imgUrl,
            role: this.user.role,
            depart_id: this.user.depart_id,
            depart_name: this.user.depart_name,
            position_id: this.user.position_id,
            address: this.user.address,
            marital_status: this.user.marital_status,
            phoneNumber: this.user.phoneNumber,
            birthday: this.user.birthday,
            gender: this.user.gender,
            numberCard: this.user.numberCard,
            nationality: this.user.nationality,
            ethnic: this.user.ethnic,
            religion: this.user.religion,
            educationalLevel: this.user.educationalLevel,
            degree: this.user.degree,
            academicLevel: this.user.academicLevel,
          });
          localStorage.setItem("employee", JSON.stringify(resDataEm));
          this.employee = resDataEm;
          //User
          const detailsUser = resDataUser[this.editedIndex];
          resDataUser.splice(this.editedIndex, 1, {
            id: detailsUser.id,
            email: detailsUser.email,
            password: detailsUser.password,
            firstName: this.user.firstName,
            lastName: this.user.lastName,
            role: this.user.role,
            timeLogin: detailsUser.timeLogin,
          });
          localStorage.setItem("user", JSON.stringify(resDataUser));
          //Payment
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
              fullName: this.user.lastName + " " + this.user.firstName,
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
        let result = Object.values(this.user);
        if (result.length < 16) {
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
              password: "12345678",
              firstName: this.user.firstName,
              lastName: this.user.lastName,
              role: this.user.role,
              timeLogin: today.toLocaleString(),
            });
            localStorage.setItem("user", JSON.stringify(resUser));
            const resEm = JSON.parse(localStorage.getItem("employee"));
            const detailsIdEm = resEm[resEm.length - 1];
            resEm.push({
              id: detailsIdEm.id + 1,
              emp_ID: `NV${detailsIdEm.id + 1}`,
              firstName: this.user.firstName,
              lastName: this.user.lastName,
              email: this.user.email,
              password: "12345678",
              role: this.user.role,
              position_id: this.user.position_id,
              depart_id: this.user.depart_id,
              depart_name: this.user.depart_name,
              address: this.user.address,
              marital_status: this.user.marital_status,
              imgUrl: this.user.imgUrl,
              phoneNumber: this.user.phoneNumber,
              birthday: this.user.birthday,
              gender: this.user.gender,
              numberCard: this.user.numberCard,
              nationality: this.user.nationality,
              ethnic: this.user.ethnic,
              religion: this.user.religion,
              educationalLevel: this.user.educationalLevel,
              degree: this.user.degree,
              academicLevel: this.user.academicLevel,
            });
            this.employee = resEm;
            localStorage.setItem("employee", JSON.stringify(resEm));
            this.dialog = false;
            this.showDialogCreateSuccess = true;
          }
        }
      }
    },
    cancel() {
      this.showDialogDelete = false;
      this.showDialogDeleteSuccess = false;
      this.showDialogCreateRequired = false;
      this.showDialogCreateSuccess = false;
      this.showDialogDuplicateEmail = false;
      this.showDialogUpdate = false;
    },
    confirm() {
      this.showDialogDelete = false;
      this.showDialogDeleteSuccess = false;
      this.showDialogCreateRequired = false;
      this.showDialogCreateSuccess = false;
      this.showDialogDuplicateEmail = false;
      this.showDialogUpdate = false;
    },
    showPassword() {
      this.$store.dispatch("actionSetShowPassword");
    },
  },
  async mounted() {
    // const res = await axios.get(`${process.env.VUE_APP_SERVER_URL}/employee`);
    const res = JSON.parse(localStorage.getItem("employee"));
    this.employee = res;

    // const resPo = await axios.get(`${process.env.VUE_APP_SERVER_URL}/position`);
    const resPo = JSON.parse(localStorage.getItem("position"));
    let result = resPo.map((a) => a.role);
    this.listRole = result;
    // const resDe = await axios.get(`${process.env.VUE_APP_SERVER_URL}/departments`);
    const resDe = JSON.parse(localStorage.getItem("departments"));
    let resultDe = resDe.map((a) => a.depart_name);
    this.listDepartment = resultDe;
  },
  computed: {
    ...mapState({
      choose: (state) => state.choose,
      visibility: (state) => state.visibility,
    }),
    formTitle() {
      return this.editedIndex === -1
        ? "Thêm mới nhân viên"
        : "Sửa thông tin nhân viên";
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
.v-data-table >>> td:nth-of-type(8) {
  max-width: 330px;
}
.v-data-table >>> td {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
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
