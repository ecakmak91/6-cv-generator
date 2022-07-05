<template>
  <div class="container">
    <div class="overlay">
      <form class="default-form personal-information-form">
        <div class="item fullwidth"> 
          <input type="file">
          <img :src="person.image" alt="">
        </div>
        <div class="item">
          <span class="lbl">Name</span>
          <input type="text" v-model="person.name" placeholder="Name">
        </div>
        <div class="item">
          <span class="lbl">Surname</span>
          <input type="text" v-model="person.surname" placeholder="Surnome">
        </div>
        <div class="item">
          <span class="lbl">Birth Date</span>
          <input type="date" v-model="person.birthDate" placeholder="Birth Date">
        </div>
        <div class="item">
          <span class="lbl">Address</span>
          <input type="text" v-model="person.address" placeholder="Address">
        </div>
        <div class="item">
          <span class="lbl">Phone</span>
          <the-mask :mask="'+90 (5##) ###-####'" v-model="person.phone" placeholder="+90 (5##) ###-####"/>
        </div>
        <div class="item">
          <span class="lbl">E-Mail</span>
          <input type="text" v-model="person.mail" placeholder="Mail">
        </div>
        <div class="item">
          <span class="lbl">City</span>
          <input type="text" v-model="person.city" placeholder="City">
        </div>
        <div class="item">
          <span class="lbl">Country</span>
          <input type="text" v-model="person.country" placeholder="Country">
        </div>
      </form>
      <hr>
      <form class="default-form social-form">
        <h3>Social Platforms</h3>
        <div class="item fullwidth">
          <ul v-if="person.socials.length>0">
            <li>
              <h5>Platform</h5>
              <h5>Link</h5>
            </li>
            <li v-for="(item,index) in person.socials" :key="index">
              <p>{{item.name}}</p>
              <p>{{item.url}}</p>
            </li>
          </ul>
          <div class="form-group">
            <div class="input-group">
              <input type="text" v-model="tmpSocials.name" placeholder="Platform">
              <input type="text" v-model="tmpSocials.url" placeholder="https://">
            </div>
            <a @click="pushToArray(person.socials,tmpSocials)">Add</a>
          </div>
        </div>
        
      </form>
      <hr>
      <form class="default-form languages-form">
        <h3>Languages</h3>
        <div class="item fullwidth">
          <ul v-if="person.languages.length>0">
            <li>
              <h5>Language</h5>
              <h5>Experience</h5>
            </li>
            <li v-for="(item,index) in person.languages" :key="index">
              <p>{{item.name}}</p>
              <p>{{item.stars}}</p>
            </li>
          </ul>
          <div class="form-group">
            <div class="input-group">
              <input type="text" v-model="tmpLanguages.name" placeholder="Language">
              <select v-model="tmpLanguages.stars">
                <option value="">Level</option>
                <option value="Conversational">Conversational</option>
                <option value="Intermediate">Intermediate</option>
                <option value="Advanced">Advanced</option>
                <option value="Fluent">Fluent</option>
                <option value="Bilingual">Bilingual</option>
                <option value="Native">Native</option>
              </select>
              

            </div>
            <a @click="pushToArray(person.languages,tmpLanguages)">Add</a>
          </div>

        </div>
      </form>
      <hr>
      <form class="default-form workHistories-form">
        <h3>Work Histories</h3>
        <div class="item fullwidth">
          <ul>
            <li v-for="(item,index) in person.workHistories" :key="index">
              {{item}}
            </li>
          </ul>
          <input type="date" v-model="tmpWorkHistories.startDate" placeholder="Start Date">
          <input type="date" v-model="tmpWorkHistories.endDate"  placeholder="End Date">
          <input type="text" v-model="tmpWorkHistories.postion"  placeholder="Position">
          <input type="text" v-model="tmpWorkHistories.description"  placeholder="Description">
          <a @click="pushToArray(person.workHistories,tmpWorkHistories)">Add</a>
        </div>
      </form>
      <hr>
      <form class="default-form education-form">
        <h3>Educational History</h3>
        <div class="item fullwidth">
          <ul>
            <li v-for="(item,index) in person.educations" :key="index">
              {{item}}
            </li>
          </ul>
          <input type="date" v-model="tmpEducations.startDate" placeholder="Start Date">
          <input type="date" v-model="tmpEducations.endDate" placeholder="End Date">
          <input type="text" v-model="tmpEducations.schooll" placeholder="Scholl">
          <input type="text" v-model="tmpEducations.bechalorDegree" placeholder="Bechalor Degree">
          <input type="text" v-model="tmpEducations.faculty" placeholder="Faculty">
          <input type="text" v-model="tmpEducations.department" placeholder="Department">
          <a @click="pushToArray(person.educations,tmpEducations)">Add</a>
        </div>
      </form>
      <hr>
      <form class="default-form courses-form">
        <h3>Courses</h3>
        <div class="item fullwidth">
          <ul>
            <li v-for="(item,index) in person.courses" :key="index">
              {{item}}
            </li>
          </ul>
          <input type="text" v-model="tmpCourses.name" placeholder="Name">
          <input type="text" v-model="tmpCourses.takenDate" placeholder="Date">
          <input type="text" v-model="tmpCourses.file" placeholder="File">
          <a @click="pushToArray(person.courses,tmpCourses)">Add</a>
        </div>
      </form>
      <hr>
      <form class="default-form technicalKnowHow-form">
        <h3>Technical Know Hows</h3>
        <div class="item fullwidth">
          <ul>
            <li v-for="(item,index) in person.technicalKnowHows" :key="index">
              {{item}}
            </li>
          </ul>
          <input type="text" v-model="tmpTechnicalKnowHows.skills" placeholder="Skills">
          <input type="text" v-model="tmpTechnicalKnowHows.stars" placeholder="Experience">
          <a @click="pushToArray(person.technicalKnowHows,tmpTechnicalKnowHows)">Add</a>
        </div>
      </form>
      <hr>
      <div class="default-form workedProjects-form">
        <h3>Worked Projects</h3>
        <div class="item fullwidth">
          <ul>
            <li v-for="(item,index) in person.workedProjects" :key="index">
              {{item}}
            </li>
          </ul>
          <input type="text" v-model="tmpWorkedProjects.name" placeholder="Project Name">
          <input type="text" v-model="tmpWorkedProjects.position" placeholder="Position">
          <input type="text" v-model="tmpWorkedProjects.url" placeholder="Url">
          <input type="text" v-model="tmpWorkedProjects.year" placeholder="Year">
          <a @click="pushToArray(person.workedProjects,tmpWorkedProjects)">Add</a>
        </div>
      </div>
      <hr>
      <div class="bottom">
        <a @click="previewClick">
          <span class="material-symbols-outlined">arrow_back_ios_new</span>
        </a>
        <a @click="nextClick">
          <span class="material-symbols-outlined">arrow_forward_ios</span>
        </a>
      </div>
    </div>
    <div class="preview">
      {{person}}
    </div>
  </div>
</template>

<script>
import {TheMask} from 'vue-the-mask'

/*
  linkedin:"",
  twitter:"",
  medium:"",
  facebook:"",
  github:"",
  instagram:"",
  behance:""
*/
export default {
  components: {TheMask},
  data(){
    return {
      tmpSocials:{
        name:"",
        url:""
      },
      tmpLanguages:{
        name:"",
        stars:""
      },
      tmpWorkHistories:{
        startDate:"",
        endDate:"",
        postion:"",
        description:""
      },
      tmpEducations:{
        startDate:"",
        endDate:"",
        schooll:"",
        bechalorDegree:"",
        faculty:"",
        department:""
      },
      tmpCourses:{
        name:"",
        takenDate:"",
        file:""
      },
      tmpProfessionalSkills:{
        name:""
      },
      tmpTechnicalKnowHows:{
          skills:"",
          stars:""
      },
      tmpWorkedProjects:{
          name:"",
          position:"",
          url:"",
          year:""
      },
      person:{
        name:"Emre",
        surname:"Çakmak",
        birthDate:"",
        address:"",
        phone:"",
        mail:"",
        image:"",
        city:"",
        country:"",
        socials:[],
        languages:[],
        workHistories:[],
        educations:[],
        courses:[],
        professionalSkills:[],
        technicalKnowHows:[],
        workedProjects:[]
      }
    }
  },
  methods:{
    fillPerson(item){
      let obj=new Object;
      for (const [key, value] of Object.entries(item)) {
        obj[key]=value
      }
      return obj;
    },
    pushToArray(elem,tmpObj){
      let tmpObjItem = new this.fillPerson(tmpObj);

      elem.push(tmpObjItem)
      for (const [key, value] of Object.entries(tmpObj)) {
        tmpObj[key]=""
      }
    },
    previewClick(){

    },
    nextClick(){

    }
  }
}
</script>

<style>

  input,select{
    display:block;
    width: 100%;
    border: none;
    border-bottom: 1px solid #ddd;
    padding: 0 0 5px 0;
  }
  input:focus{
    
  }
  input:focus + .item::after{
    
  }
  input[type=text],input[type=date]{

  }
  input:disabled{
    background: red;
  }
  .default-form{
    margin-top: 30px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .default-form .item{
    margin-top: 15px;
    width:49%;
  }
  .default-form .item a{
    cursor: pointer;
  }
  .default-form .item:after{
    content: "";
  }
  .default-form .item.fullwidth{
    width: 100%;
  }
  .default-form .item input{
    width: 100%;
  }
  .default-form .item .lbl{
    font-size: 12px;
    font-weight: 600;
  }
  .default-form ul{
    
  }
  .default-form ul li{
    list-style: none;
  }
  .default-form ul {
    margin: 0;
    padding: 0;
  }

  .default-form ul li{
    display: flex;
  }
  .default-form ul li h5,
  .default-form ul li p {
    min-width: 30%;
  }
  .form-group{
    display: flex;
  }
  .form-group .input-group{
    position: relative;
    display: flex;
    flex-wrap: wrap;
    align-items: stretch;
    width: 100%;
  }
  .form-group a{
    background: #43c0ff;
    border: 2px solid #43c0ff;
    width: 74px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 600;
    transition: .3s;
  }
  .form-group a:hover{
    background: #fff;
  }

</style>
