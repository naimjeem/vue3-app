<template>
  <div class="container m-6">
    <div class="row justify-content-between">
        <div class="col-4">
          <h2>Sorting Traning System</h2>
        </div>
        <div class="col-4">
          <button class="btn btn-warning float-end" data-bs-toggle="modal" data-bs-target="#exampleModal">Start Sorting</button>
        </div>
    </div>
    <div class="card p-6">
      <div class="row justify-content-end">
        <div class="col-6">
          <strong class="float-end">{{dataList.length}} people in the list </strong>
        </div>
      </div>
      <table class="table">
        <thead>
          <tr>
            <th>Email</th>
            <th>Potatos</th>
            <th>Tags</th>
            <th>Fullname</th>
            <th>Location</th>
            <th>Date</th>
          </tr>
        </thead>
        <!-- <tbody> -->
          <draggable class="" :list="dataList" tag="tbody">
            <tr class="py-6" style="cursor: move; padding: 20px 10px" v-for="item in dataList" :key="item.index" draggable="true">
              <td>
                <div class="form-check">
                  <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault">
                  <label class="form-check-label" for="flexCheckDefault">
                    {{item.email}}
                  </label>
                </div>
              </td>
              <td>{{item.count}}</td>
              <td><span class="chips">{{item.tags}}</span></td>
              <td>{{item.fullName}}</td>
              <td>{{item.location}}</td>
              <td>{{item.date}}</td>
            </tr>
          </draggable>
        <!-- </tbody> -->
      </table>

    </div>
  </div>

  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div v-if="!isLoaded">
          <div class="modal-header">
            <h5 class="modal-title fw-bold" id="exampleModalLabel">How Many People</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <div class="mb-3">
              <label for="exampleFormControlInput1" class="form-label">Enter a number of how many people you want to add to the list.</label>
              <input type="number" class="form-control" v-model="count" id="exampleFormControlInput1" placeholder="20" :min="20" :max="100">
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-default" data-bs-dismiss="modal">Close</button>
            <button type="button" class="btn btn-warning" @click="generateData()">Start</button>
          </div>
        </div>
      </div>
      <div class="alert alert-success" role="alert" v-if="isLoaded">
        <h3>Successfully Generated {{count}} Peoples</h3>
      </div>
    </div>
  </div>
</template>

<script>
import faker from 'faker'
import { VueDraggableNext } from 'vue-draggable-next'

export default {
  components: {
    draggable: VueDraggableNext,
  },
  data: () => {
    return {
      total: 20,
      count: '20',
      dataList: [],
      isLoading: false,
      isLoaded: false
    }
  },
  methods: {
    init() {
      for (let i = 1; i <= 20; i++) {

        let email = faker.internet.email();
        let count = faker.random.number(50);
        let tags = faker.random.objectElement(['Customer', 'VIP', 'Social', 'Important'])
        let fullName = faker.name.firstName() + ' ' + faker.name.lastName();
        let location = faker.address.country();
        let date = faker.date.between('2020-01-01', '2025-12-31').toISOString()

        const item = {
            email,
            count,
            tags,
            fullName,
            location,
            date
        }
        this.dataList.push(item);
      }

      console.log(JSON.parse(JSON.stringify(this.dataList)));
      return JSON.parse(JSON.stringify(this.dataList))
    },
    generateData() {
      this.isLoading = true;
      for (let i = 1; i <= this.count; i++) {

        let email = faker.internet.email();
        let count = faker.random.number(50);
        let tags = faker.random.objectElement(['Customer', 'VIP', 'Social', 'Important'])
        let fullName = faker.name.firstName() + ' ' + faker.name.lastName();
        let location = faker.address.country();
        let date = faker.date.between('2020-01-01', '2025-12-31').toISOString()

        const item = {
            email,
            count,
            tags,
            fullName,
            location,
            date
        }
        this.dataList.push(item);
        // console.log(item);
      }

      console.log(JSON.parse(JSON.stringify(this.dataList)));
      this.isLoading = false;
      this.isLoaded = true;
      setTimeout(() => {
        this.isLoaded = false;
      }, 3000);
      return JSON.parse(JSON.stringify(this.dataList))
    }
  },
  mounted() {
    this.init();
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin: 60px;
}
.card {
  padding: 20px;
}
button.btn-default {
  background: lightgray;
}
button.btn-warning {
  color: #eeeeee;
}
table {
  font-size: 14px;

}
th {
  color: #555555;
}
tbody.tr:hover {
  cursor: move;
}
tr {
  padding: 20px 10px !important;
}
td {
  padding-top:20px;
  padding-bottom:20px;
  padding-right:20px;
}

.chips {
  background: #eeeeee;
  color: #555555;
  padding: 10px;
  border-radius: 16px;
  margin: 20px 0;
}
.form-check-input:checked {
  background-color: #FF8D00 !important;
  border-color: #FF8D00 !important;
}
</style>
