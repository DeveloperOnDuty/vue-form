<template>
    <div>
        <form @submit.prevent="handleSubmit">
            <label> Email: </label>
            <input type="email" v-model="email" required>

            <label> Password: </label>
            <input type="password" v-model="password" required>
            <div class="error" v-if="passwordError">{{passwordError}}</div>

            <label> Role: </label>
            <select v-model="role" >
                <option value="Front-end developer">Front-end developer</option>
                <option value="UI/UX developer">UI/UX developer</option>
                <option value="Back-end developer">Back-end developer</option>
            </select>

            <label> Skills: </label>
            <input type="text" v-model="tempSkills" @keyup="addSkills">
            <div v-for="skill in skills" :key="skill" class="pill">
                <span @click="deleteSkill(skill)">{{ skill }}</span>
            </div>

            <div class="terms">
                <input type="checkbox" v-model="terms" required>
                <label> Accept terms and conditions</label>
            </div>
            <div class="submit">
                <button>Create An Account</button>
            </div>
        </form>
        <p>Email: {{email}}</p>
        <p>password: {{password}}</p>
        <p>Role: {{role}}</p>
        <p>Terms accepted: {{ terms }}</p>

    </div>
</template>
<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkills(e) {
            if(e.which === 13 && this.tempSkills){
                if(!this.skills.includes(this.tempSkills)) {
                    this.skills.push(this.tempSkills)
                }
                this.tempSkills = ''
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit(){
            //validate password
            this.passwordError = this.password.length > 5 ? '' : 'Password is less than 5 characters'
            if(!this.passwordError) {
                console.log('email', this.email)
                console.log('password', this.password)
                console.log('role', this.role)
                console.log('skills', this.skills)
                console.log('terms accepted', this.terms)


            }
        
        }
    }
}
</script>





<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: #ddd;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label {
    color: #333;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input,select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
.submit {
    text-align: center;
}
.submit button {
    background: cadetblue;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: #fff;
    border-radius: 20px;
}
.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>