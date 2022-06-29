<template>
  <div class="home">
    <v-container class="mt-5">
      <v-row>
        <v-col cols="12" sm="4">
          <v-hover v-slot="{ hover }" open-delay="200">
            <v-card color="cyan darken-1" :elevation="hover ? 16 : 2">
              <v-row>
                <v-col cols="12" sm="8">
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="mb-4">
                        <v-btn fab color="cyan lighten-2" elevation="0">
                          <v-icon color="white">fab fa-bitcoin</v-icon>
                        </v-btn>
                      </div>
                      <v-list-item-title class="headline mb-1 white--text">
                        2 tỷ 700 triệu
                      </v-list-item-title>
                      <v-list-item-subtitle class="white--text"
                        >Doanh Thu Công Ty</v-list-item-subtitle
                      >
                    </v-list-item-content>
                  </v-list-item>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-avatar size="100" class="ml-n10 mt-6" tile>
                    <v-img src="wallet.png"></v-img>
                  </v-avatar>
                </v-col>
              </v-row>
            </v-card>
          </v-hover>
        </v-col>
        <v-col cols="12" sm="4">
          <v-hover v-slot="{ hover }" open-delay="200">
            <v-card color="pink darken-1" :elevation="hover ? 16 : 2">
              <v-row>
                <v-col cols="12" sm="8">
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="mb-4">
                        <v-btn fab color="pink lighten-2" elevation="0">
                          <v-icon color="white">fas fa-rupee-sign</v-icon>
                        </v-btn>
                      </div>
                      <v-list-item-title class="headline mb-1 white--text">
                        400 mặt hàng
                      </v-list-item-title>
                      <v-list-item-subtitle class="white--text"
                        >Số Lượng CSVC</v-list-item-subtitle
                      >
                    </v-list-item-content>
                  </v-list-item>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-avatar size="100" class="ml-n10 mt-6" tile>
                    <v-img src="wallet.png"></v-img>
                  </v-avatar>
                </v-col>
              </v-row>
            </v-card>
          </v-hover>
        </v-col>
        <v-col cols="12" sm="4">
          <v-hover v-slot="{ hover }" open-delay="200">
            <v-card color="orange darken-1" :elevation="hover ? 16 : 2">
              <v-row>
                <v-col cols="12" sm="8">
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="mb-4">
                        <v-btn fab color="orange lighten-2" elevation="0">
                          <v-icon color="white">fas fa-pound-sign</v-icon>
                        </v-btn>
                      </div>
                      <v-list-item-title class="headline mb-1 white--text">
                        500 nhân viên
                      </v-list-item-title>
                      <v-list-item-subtitle class="white--text"
                        >Tổng số lượng nhân viên</v-list-item-subtitle
                      >
                    </v-list-item-content>
                  </v-list-item>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-avatar size="100" class="ml-n10 mt-6" tile>
                    <v-img src="wallet.png"></v-img>
                  </v-avatar>
                </v-col>
              </v-row>
            </v-card>
          </v-hover>
        </v-col>
      </v-row>
      <v-row class="mt-6">
        <v-col cols="12" sm="4">
          <v-hover v-slot="{ hover }" open-delay="200">
            <v-card color="red darken-1" :elevation="hover ? 16 : 2">
              <v-row>
                <v-col cols="12" sm="8">
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="mb-4">
                        <v-btn fab color="red lighten-2" elevation="0">
                          <v-icon color="white">fab fa-bitcoin</v-icon>
                        </v-btn>
                      </div>
                      <v-list-item-title class="headline mb-1 white--text">
                        500 triệu
                      </v-list-item-title>
                      <v-list-item-subtitle class="white--text"
                        >Tổng Giá Trị CSVC</v-list-item-subtitle
                      >
                    </v-list-item-content>
                  </v-list-item>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-avatar size="100" class="ml-n10 mt-6" tile>
                    <v-img src="wallet.png"></v-img>
                  </v-avatar>
                </v-col>
              </v-row>
            </v-card>
          </v-hover>
        </v-col>
        <v-col cols="12" sm="4">
          <v-hover v-slot="{ hover }" open-delay="200">
            <v-card color="blue darken-1" :elevation="hover ? 16 : 2">
              <v-row>
                <v-col cols="12" sm="8">
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="mb-4">
                        <v-btn fab color="blue lighten-2" elevation="0">
                          <v-icon color="white">fas fa-rupee-sign</v-icon>
                        </v-btn>
                      </div>
                      <v-list-item-title class="headline mb-1 white--text">
                        800 triệu
                      </v-list-item-title>
                      <v-list-item-subtitle class="white--text"
                        >Tổng tiền lương nhân viên CTY</v-list-item-subtitle
                      >
                    </v-list-item-content>
                  </v-list-item>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-avatar size="100" class="ml-n10 mt-6" tile>
                    <v-img src="wallet.png"></v-img>
                  </v-avatar>
                </v-col>
              </v-row>
            </v-card>
          </v-hover>
        </v-col>
        <v-col cols="12" sm="4">
          <v-hover v-slot="{ hover }" open-delay="200">
            <v-card color="green darken-1" :elevation="hover ? 16 : 2">
              <v-row>
                <v-col cols="12" sm="8">
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="mb-4">
                        <v-btn fab color="green lighten-2" elevation="0">
                          <v-icon color="white">fas fa-pound-sign</v-icon>
                        </v-btn>
                      </div>
                      <v-list-item-title class="headline mb-1 white--text">
                        70 phòng
                      </v-list-item-title>
                      <v-list-item-subtitle class="white--text"
                        >Tổng số lượng phòng ban</v-list-item-subtitle
                      >
                    </v-list-item-content>
                  </v-list-item>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-avatar size="100" class="ml-n10 mt-6" tile>
                    <v-img src="wallet.png"></v-img>
                  </v-avatar>
                </v-col>
              </v-row>
            </v-card>
          </v-hover>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" sm="6">
          <v-card>
            <v-app-bar flat color="rgba(0,0,0,0)">
              <v-toolbar-title class="title black--text pl-0 ml-2">
                Doanh Thu
              </v-toolbar-title>
              <v-spacer></v-spacer>
              <v-btn color="deep-purple" class="white--text mr-2">Theo tuần</v-btn>
              <v-btn color="deep-purple lighten-4" class="deep-purple--text "
                >Theo tháng</v-btn
              >
            </v-app-bar>
            <v-sparkline
              :fill="fill"
              :line-width="width"
              :padding="padding"
              :smooth="radius || false"
              :value="value"
              auto-draw
              color="deep-purple"
            ></v-sparkline>
          </v-card>
        </v-col>
        <v-col cols="12" sm="6">
          <v-card style="padding-bottom:9px">
            <v-app-bar flat color="rgba(0,0,0,0)" class="pb-0">
              <v-toolbar-title class="title black--text pl-0 ml-2">
                Cơ Sở Vật Chất gần đây
              </v-toolbar-title>
            </v-app-bar>
            <v-app-bar flat color="rgba(0,0,0,0)" style="margin-top:-8px">
              <v-btn
                fab
                color="red lighten-2"
                elevation="0"
                width="50"
                height="50"
                class="me-3"
              >
                <v-icon color="red">fab fa-bitcoin</v-icon>
              </v-btn>
              <v-toolbar-title class="title black--text ml-2">
                Bàn Gỗ <span class="caption"><br />Số Lượng: 10</span>
              </v-toolbar-title>
              <v-spacer></v-spacer>
              <v-toolbar-title class="subtitle-1 black--text ml-2">
                -10.000.000đ
              </v-toolbar-title>
              <v-icon color="green" class="ml-2">fas fa-long-arrow-alt-up</v-icon>
            </v-app-bar>
            <v-app-bar flat color="rgba(0,0,0,0)">
              <v-btn
                fab
                color="yellow lighten-2"
                elevation="0"
                width="50"
                height="50"
                class="me-3"
              >
                <v-icon color="yellow">fas fa-yen-sign</v-icon>
              </v-btn>
              <v-toolbar-title class="title black--text ml-2">
                Máy Chiếu Xiaomi <span class="caption"><br />Số Lượng: 20</span>
              </v-toolbar-title>
              <v-spacer></v-spacer>
              <v-toolbar-title class="subtitle-1 black--text ml-2">
                -40.000.000đ
              </v-toolbar-title>
              <v-icon color="red" class="ml-2">fas fa-long-arrow-alt-down</v-icon>
            </v-app-bar>
            <v-app-bar flat color="rgba(0,0,0,0)">
              <v-btn
                fab
                color="green lighten-2"
                elevation="0"
                width="50"
                height="50"
                class="me-3"
              >
                <v-icon color="green">fas fa-yen-sign</v-icon>
              </v-btn>
              <v-toolbar-title class="title black--text ml-2">
                LapTop M1 Pro <span class="caption"><br />Số Lượng: 10</span>
              </v-toolbar-title>
              <v-spacer></v-spacer>
              <v-toolbar-title class="subtitle-1 black--text ml-2">
                -300.000.000đ
              </v-toolbar-title>
              <v-icon color="red" class="ml-2">fas fa-long-arrow-alt-down</v-icon>
            </v-app-bar>
          </v-card>
        </v-col>
        <v-col cols="12" sm="6">
          <v-card height="180px">
            <v-row>
              <v-col cols="12" sm="4">
                <v-list-item three-line>
                  <v-list-item-content>
                    <div class="mb-4">Hiệu Suất Công Việc</div>
                    <v-list-item-title class="headline mb-1 black--text">
                      Doanh số tăng 20%
                    </v-list-item-title>
                    <v-list-item-subtitle class="grey--text"
                      >so với tháng 1</v-list-item-subtitle
                    >
                  </v-list-item-content>
                </v-list-item>
              </v-col>
              <v-col cols="12" sm="8">
                <v-sparkline
                  :value="value"
                  :smooth="radius || false"
                  :padding="padding"
                  :line-width="width"
                  :stroke-linecap="lineCap"
                  :fill="fills"
                  :type="type"
                  :auto-line-width="autoLineWidth"
                  auto-draw
                  color="red"
                >
                </v-sparkline>
                <v-card-actions class="justify-end">
                  <v-btn text color="green">
                    <v-icon class="mt-n2 pr-2">fas fa-sort-down</v-icon> 8.5
                  </v-btn>
                </v-card-actions>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
        <v-col cols="12" sm="6">
          <v-card>
            <v-row>
              <v-col cols="12" sm="6" class="border">
                <v-list-item three-line>
                  <v-list-item-content>
                    <div class="mb-4">Your Portfolio</div>
                    <v-row>
                      <v-col cols="12" sm="6">
                        <v-progress-circular
                          rotate="360"
                          size="100"
                          width="15"
                          value="70"
                          color="teal"
                        >
                          70%
                        </v-progress-circular>
                      </v-col>
                      <v-col cols="12" sm="6">
                        <v-list-item-subtitle class="grey--text mt-8"
                          >2.5578 BTC</v-list-item-subtitle
                        >
                        <v-list-item-subtitle class="grey--text"
                          >2500 USD</v-list-item-subtitle
                        >
                      </v-col>
                    </v-row>
                  </v-list-item-content>
                </v-list-item>
              </v-col>
              <v-col cols="12" sm="6" align="center">
                <v-list-item two-line class="mt-10">
                  <v-list-item-content>
                    <v-list-item-title class="headline mb-1 black--text">
                      $8520.50
                    </v-list-item-title>
                    <v-list-item-subtitle class="grey--text"
                      >Pending Balance</v-list-item-subtitle
                    >
                  </v-list-item-content>
                </v-list-item>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
        <v-col cols="12" sm="12" align="center">
          <v-card style="margin-top: -8px">
            <v-data-table
              caption="Danh Sách Nhân Viên Xuất Xắc"
              :headers="headers"
              :items="desserts"
              :items-per-page="5"
              class="elevation-1"
            >
              <template v-slot:[`item.actions`]="">
                <v-btn color="success" outlined small shaped>View</v-btn>
              </template>
            </v-data-table>
          </v-card>
        </v-col>
        <v-col cols="12" sm="12" align="center">
          <v-card style="margin-top: -8px">
            <v-data-table
              caption="Danh Sách Phòng Ban Xuất Xắc"
              :headers="departmentHeaders"
              :items="departmentDesserts"
              :items-per-page="5"
              class="elevation-1"
            >
              <template v-slot:[`item.actions`]="">
                <v-btn color="success" outlined small shaped>View</v-btn>
              </template>
            </v-data-table>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Report",
  data: () => ({
    tab: null,
    text: "center",
    fill: true,
    padding: 8,
    radius: 10,
    value: [0, 2, 5, 9, 5, 10, 3, 5, 0, 0, 1, 8, 2, 9, 0],
    width: 2,
    lineCap: "round",
    type: "trend",
    autoLineWidth: false,
    fills: false,
    headers: [
      {
        text: "ID",
        align: "center",
        sortable: false,
        value: "id",
      },
      { text: "Tên Nhân Viên", align: "center", value: "nameEm" },
      { text: "Chức Vụ", align: "center", value: "position" },
      { text: "Phòng Ban", align: "center", value: "department" },
      { text: "Email", align: "center", value: "email" },
      { text: "Thành Tích", align: "center", value: "performance" },
    ],
    departmentHeaders: [
      {
        text: "ID",
        align: "center",
        sortable: false,
        value: "id",
      },
      { text: "Mã Phòng Ban", align: "center", value: "deId" },
      { text: "Tên Phòng Ban", align: "center", value: "deName" },
      { text: "Địa Chỉ", align: "center", value: "address" },
      { text: "Trưởng Phòng", align: "center", value: "deHead" },
      { text: "Thành Tích", align: "center", value: "performance" },
    ],
    desserts: [
      {
        id: 1,
        nameEm: "Nguyễn Sỹ Dũng",
        position: "Admin",
        department: "Phòng Cơ Sở Vật Chất",
        email: "sydung@gmail.com",
        performance: "Admin tốt nhất công ty",
      },
      {
        id: 2,
        nameEm: "Trần Hữu Lương",
        position: "Nhân Viên",
        department: "Phòng Cơ Sở Vật Chất",
        email: "luongtran@gmail.com",
        performance: "Nhân Viên năng động nhất công ty",
      },
      {
        id: 3,
        nameEm: "Võ Trung Hiếu",
        position: "Nhân Viên",
        department: "Phòng Cơ Sở Vật Chất",
        email: "hieuvo@gmail.com",
        performance: "Nhân Viên hài hước nhất công ty",
      },
      {
        id: 4,
        nameEm: "Dương Thị Thùy Dung",
        position: "Nhân Viên",
        department: "Phòng Cơ Sở Vật Chất",
        email: "thuydung@gmail.com",
        performance: "Nhân Viên siêng năng nhất công ty",
      },
      {
        id: 5,
        nameEm: "Lê Doãn Chánh",
        position: "Trưởng Phòng",
        department: "Phòng Cơ Sở Vật Chất",
        email: "doanchanh@gmail.com",
        performance: "Trưởng Phòng 5 tốt",
      },
    ],
    departmentDesserts: [
      {
        id: 1,
        deId: "CNTT7",
        deName: "Phòng Công Nghệ Thông Tin",
        address: "Phòng 202",
        deHead: "Trần Hữu Lương",
        performance: "Hoàn thành tốt dự án JAPAN",
      },
      {
        id: 2,
        deId: "CNTT7",
        deName: "Phòng Công Nghệ Thông Tin",
        address: "Phòng 202",
        deHead: "Trần Hữu Lương",
        performance: "Hoàn thành tốt dự án JAPAN",
      },
      {
        id: 3,
        deId: "CNTT7",
        deName: "Phòng Công Nghệ Thông Tin",
        address: "Phòng 202",
        deHead: "Trần Hữu Lương",
        performance: "Hoàn thành tốt dự án JAPAN",
      },
      {
        id: 4,
        deId: "CNTT7",
        deName: "Phòng Công Nghệ Thông Tin",
        address: "Phòng 202",
        deHead: "Trần Hữu Lương",
        performance: "Hoàn thành tốt dự án JAPAN",
      },
      {
        id: 5,
        deId: "CNTT7",
        deName: "Phòng Công Nghệ Thông Tin",
        address: "Phòng 202",
        deHead: "Trần Hữu Lương",
        performance: "Hoàn thành tốt dự án JAPAN",
      },
    ],
  }),
};
</script>
<style lang="sass" scoped>
.v-card.on-hover.theme--dark
  background-color: rgba(#FFF, 0.8)
  >.v-card__text
    color: #000
</style>
<style scoped>
.border {
  border-right: 1px solid grey;
}
.elevation-1 {
  padding-top: 20px !important;
}
</style>
