<template>
  <v-layout class="background" align-center justify-center>
    <div class="form">
      <v-text-field v-model="form.id" label="아이디"></v-text-field>
      <v-text-field
        v-model="form.password"
        type="password"
        label="패스워드"
      ></v-text-field>

      <!--
      <v-btn class="mr-2" @click="login">로그인</v-btn>
      css에서는 -이 하나의 표식으로 인식되기 때문에 변경!--> 
      <!-- 아이디, 패스워드 입력하고 로그인 버튼 누르면 버튼 배경색이 변경됨-->
      <mjc-btn  :background="loginbtnBg" fontcolor="white" @click="login" @changeBackground="loginBtnBackground"> 로그인 </mjc-btn>
      <mjc-btn class="mt-s" background="#0000ff" fontcolor="white" @click="moveJoin"> 회원가입 </mjc-btn>
      <!--<v-btn @click="moveJoin">회원가입</v-btn>!-->
    </div>
  </v-layout>
</template>


<script>
import HelloWorld from "../components/HelloWorld";  //..은 상대 경로를 사용(상위디렉토리의)
import MjcBtn from "@/components/MjcBtn";  //@는 src 폴더(를 기준으로 import)

export default {
  components:{
    MjcBtn
  },
  name: "Home",
  data() {
    return {
      loginbtnBg: "#ff0000",
      form: {
        id: "",
        password: "",
      },
      name: "",
    };
  },
  methods: {
    loginBtnBackground(background){
      this.loginbtnBg=background;
    },
    login(background) {
      //TODO : 폼체크하는 거 추가해야 됨
      if (this.form.id == "") {
        window.alert("아이디를 입력해주세요");
        return;
      }
      if (this.form.password.length < 8) {
        window.alert("패스워드는 8자 이상이어야 합니다");
        return;
      }
      //TODO : 서버에 전송해서 로그인 시키기
      this.axios.post("/api/users/login", this.form).then((result) => {
        // 로그인 성공
        if (result.data.result == "ok") {
          console.log(result.data.user);
          this.$store.commit("setUser", result.data.user); // 로그인한 정보를 user로 보내고 저장하는 함수
          this.$router.push("/board");
        }
        // 로그인 실패
        if (result.data.result == "fail") {
          window.alert(result.data.message);
        }
      });
      //this.$router.push("/board");
    },
    moveJoin() {
      this.$router.push("/join");
    },
  },
};
</script>
<style scoped>
.background {
  background: #eeeeee;
}
.background .form {
  background: white;
  padding: 20px;
  border-radius: 10px;
}
</style>