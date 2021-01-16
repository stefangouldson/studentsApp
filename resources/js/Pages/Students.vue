<template>
  <div>
    <app-layout>
      <template #header>
        <h2 class="font-semibold text-xl text-gray-800 leading-tight">
          Students
        </h2>
      </template>

      <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
          <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
            <!-- This example requires Tailwind CSS v2.0+ -->
            <div class="flex flex-col">
              <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                <div
                  class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8"
                >
                  <div
                    class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg"
                  >
                    <table class="min-w-full divide-y divide-gray-200">
                      <thead class="bg-gray-50">
                        <tr>
                          <th
                            scope="col"
                            class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                          >
                            Full Name
                          </th>
                          <th
                            scope="col"
                            class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                          >
                            Course
                          </th>
                          <th
                            scope="col"
                            class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                          >
                            Date of Enrollment
                          </th>
                          <th scope="col" class="relative px-6 py-3">
                            <span class="sr-only">Edit</span>
                          </th>
                        </tr>
                      </thead>
                      <tbody class="bg-white divide-y divide-gray-200">
                        <tr v-for="x in students" :key="x.id">
                          <td class="px-6 py-4 whitespace-nowrap">
                            <div class="flex items-center">
                              <div class="text-sm font-medium text-gray-900">
                                {{x.full_name}}
                              </div>
                            </div>
                          </td>
                          <td class="px-6 py-4 whitespace-nowrap">
                            <div class="text-sm text-gray-900">{{x.course}}</div>
                          </td>
                          <td class="px-6 py-4 whitespace-nowrap">
                            <span
                              class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800"
                            >
                             {{x.date_of_enrollment}}
                            </span>
                          </td>
                          <td
                            class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium"
                          >
                            <a
                              href="#"
                              class="text-indigo-600 hover:text-indigo-900"
                              >Edit</a
                            >
                            <br />
                            <a href="#" class="text-red-600 hover:text-red-900"
                              >Delete</a
                            >
                          </td>
                        </tr>

                        <!-- More items... -->
                      </tbody>
                    </table>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <template #footer>
        <!-- Button trigger modal -->
        <button type="button" class="btn btn-primary float-right " data-bs-toggle="modal" data-bs-target="#exampleModal">
          Add student
        </button>

        <!-- Modal -->
        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Add student</h5>
                <button
                  type="button"
                  class="btn-close"
                  data-bs-dismiss="modal"
                  aria-label="Close"
                ></button>
              </div>
              <div class="modal-body">
                  <form id="studentForm" @submit.prevent="addStudent" class="container-fluid">
                      <div class="form-group">
                          <label for="">Full Name</label>
                          <input v-model="student.full_name"  type="text" name="full_name" class="form-control" placeholder="Enter Student Name">
                      </div>
                      <div class="form-group">
                          <label for="">Course</label>
                          <select v-model="student.course"  name="course" class="form-control">
                              <option v-for="y in courses" :key="y.id" :value="y.course_name">{{y.course_name}}</option>
                          </select>
                      </div>
                        <div class="form-group">
                          <label for="">Enrollment Date</label>
                          <input type="date"  v-model="student.date_of_enrollment"  name="date_of_enrollment" class="form-control">
                      </div>
                      <div class="mt-2">
                        <button type="submit" class="btn btn-primary">
                            Save changes
                        </button>
                      </div>
                  </form>
              </div>
              <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal"> Cancel</button>
              </div>
            </div>
          </div>
        </div>

        <br>
        <br>
        <br>

                <!-- Button trigger modal -->
        <button type="button" class="btn btn-success float-right " data-bs-toggle="modal" data-bs-target="#addcourse">
          Add Course
        </button>

        <!-- Modal -->
        <div class="modal fade" id="addcourse" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Add Course</h5>
                <button
                  type="button"
                  class="btn-close"
                  data-bs-dismiss="modal"
                  aria-label="Close"
                ></button>
              </div>
              <div class="modal-body">
                  <form id="courseForm" @submit.prevent="addCourse" class="container-fluid">
                      <div class="form-group">
                          <label for="">Course Name</label>
                          <input v-model="course.course_name" type="text" name="course_name" class="form-control" placeholder="Course Name">
                      </div>
                      <div class="mt-4">
                          <button type="submit" class="btn btn-success">Add course</button>
                      </div>
                  </form>
              </div>
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-secondary"
                  data-bs-dismiss="modal"
                >
                  Close
                </button>

              </div>
            </div>
          </div>
        </div>
      </template>

    </app-layout>
  </div>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout";
import Welcome from "@/Jetstream/Welcome";

export default {
  components: {
    AppLayout,
    Welcome,
  },

  data(){
      return {
          students: [],
          student: {
              full_name:'',
              date_of_enrollment: '',
              course: ''
          },
          courses: [],
          course: {
              course_name: ''
          }
      }
    },

    methods:{
        async addStudent(){
            const res = await axios.post('/api/students', this.student)

            if(res.status === 201){
                Toast.fire({
                    icon:'success',
                    title: res.data
                })
                document.getElementById('studentForm').reset()

                this.full_name = ''
                this.date_of_enrollment = ''
                this.course = ''

                // $('#exampleModal').modal('hide')
                $('#exampleModal').hide();
                $('.modal-backdrop').hide()
                Fire.$emit('addedStudent')
            }
        },

        async addCourse(){
            const res = await axios.post('/api/courses', this.course)

            if(res.status === 201){
                Toast.fire({
                    icon:'success',
                    title: res.data
                })

                this.course.course_name = '';

                $('#addcourse').hide();
                $('.modal-backdrop').hide()

                Fire.$emit('addedCourse')
            }
        },

        getStudents(){
            axios.get('/api/students')
            .then((res)=>{
                this.students = res.data
            }).catch((err)=>{
                console.log(err)
            })
        },

        getCourses(){
            axios.get('/api/courses').then((res)=>{
                this.courses = res.data
            }).catch((err)=>{
                console.log(err)
            })
        },

    },
        created(){
            this.getCourses(),
            this.getStudents(),

            Fire.$on('addedCourse', ()=>{
                this.getCourses()
            })

            Fire.$on('addedStudent', ()=>{
                this.getStudents()
            })
        }
};
</script>
