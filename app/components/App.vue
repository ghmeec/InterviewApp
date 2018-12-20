

<template>
    <Page>
            <ActionBar title=" Question" icon="">
            </ActionBar>
        <StackLayout>
            <Label :text="qn" editable="false" class="title" />
           
           <ListView for="item in source" class="options">
                <v-template>
                    <StackLayout orientation="horizontal" class="selected">
                          <Label :text="item.option " textWrap="true" />
                          <Label text=" " textWrap="true" />
                          <Label :text="item.name " />
                    </StackLayout>
                   
                </v-template>
            </ListView>


             <TextField hint="" v-model="name" />
            <Label :text="msg" :class="{correct:isCorect,incorrect:isIncorrect}" textWrap="true" />

            <Button :text="score" class="btn rounded" />
            <Button text="Save answer" @tap="clicked" />
            <Button text="Next question" @tap="nextQuestion" />
  
        </StackLayout>
    </Page>
</template>

<script>
export default {
  data() {
    return {
      source: [
        {
          name: "A. 1991"
        },
        {
          name: "B. 1964"
        },
        {
          name: "C. 1961"
        }
      ],
      qns: [
        {
          attempted: false,
           savedState: "",
          qn: "Tanganyika independece year",
          answer: "A",
          options: [
            { option: "A", name: "1961" },
            { option: "B", name: "2014" },
            { option: "C", name: "1964" }
          ]
        },
        {
          attempted: false,
           savedState: "",
          qn: " Tanganyika and Tanzania union",
          answer: "C",
          options: [
            { option: "A", name: "1961" },
            { option: "B", name: "2014" },
            { option: "C", name: "1964" }
          ]
        },
        {
          attempted: false,
          savedState: "",
          qn: "First multiparty election in TZ",
          answer: "A",
          options: [
            { option: "A", name: "1995" },
            { option: "B", name: "1992" },
            { option: "C", name: "1967" }
          ]
        },
        {
          attempted: false,
          savedState: "",
          qn: "Nyerere died",
          answer: "B",
          options: [
            { option: "A", name: "1961" },
            { option: "B", name: "1999" },
            { option: "C", name: "2000" }
          ]
        },
        {
          attempted: false,
          savedState: "",
          qn: "Magufuli become president in ",
          answer: "B",
          options: [
            { option: "A", name: "2010" },
            { option: "B", name: "2015" },
            { option: "C", name: "2014" }
          ]
        }
      ],
      qn: "Tanganyika independence year",
      msg: "",
      name: "",
      answer: "1961",
      attempted: false,
      isCorect: false,
      isIncorrect: false,
      qnNO: 0,
      score: 0,
      state:0,
    };
  },
  methods: {
    clicked() {
      console.log("Button is clicked");
      if (this.name == "") {
        alert("Empty values not allowable").then(() => {
          console.log("Alert dialog closed.");
        });
        return;
      }

      confirm({
        title: "Confirm",
        message: "Thibitisha ",
        okButtonText: "Ndio",
        cancelButtonText: "Hapana"
      }).then(result => {
        if (!result) {
          return;
        } else {
          this.qns[this.state].savedState="Hksaad";
          console.log(this.qns[this.state].savedState)
          if (this.name == this.answer) {
            (this.msg = "Correct"), (this.isCorect = true);
            this.isIncorrect = false;
            this.score++;
          } else {
            this.msg = "Incorrect";
            this.isIncorrect = true;
            this.isCorect = false;
          }
        }
   
      });
    },
    nextQuestion() {
      console.log("Inside next question");
      if (this.qnNO >= this.qns.length - 1) {
        this.qnNO = 0;
      }

     this.state = ++this.qnNO;
      console.log(this.qnNO >= this.qns.length - 1);
      this.qn = this.qns[this.state].qn;
      this.answer = this.qns[this.state].answer;
      this.source = this.qns[this.state].options;
      if (this.qns[this.state].attempted) {
        console.log("The qn is already attempted");
        this.attempted = this.qns[this.state].attempted;
        return;
      }
      this.qns[this.state].attempted = true;
      this.attempted = this.qns[this.state].attempted;
    }
  }
};
</script>

<style scoped>
.title {
  font-size: 20;
}
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}

.correct {
  color: green;
}

.incorrect {
  color: red;
}

button {
  color: #ffffff;
  background-color: #333333;
}

.options {
  margin-left: 5%;
  width: 90%;
}
.selected{
    background-color:#333;
    color:white;
}
</style>
