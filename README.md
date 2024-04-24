let users = {
    u1:{username:'u1',password:'p1',id:1},
    u2:{username:'u2',password:'p2',id:2},
}

const Passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;


let localStrategy = new LocalStrategy({
    usernameField:'username',
    passwordFieldL:'password'
    },(username, password, done)=>{
    let user = users[username];
    if(user==null){
        return done(null,false);

    }

    if(password != user.password){
        return done(null,false);
    }
    done(null,user);
}
);

Passport.use('local', localStrategy);

const express = require('express');
const bodyParser = require('body-parser');


const app = express();
app.use(bodyParser.urlencoded({extended:false}));
app.use(bodyParser.json());
app.use(Passport.initialize());

app.use(express.static('public'));

app.post('/login',
Passport.authenticate('local',{session:false})

,(req,res)=>{
    res.send('id zalogowanego'+req.user.id);
});

const port=3000;
app.listen(port,()=>{
    console.log(`server listen on ${port}`)
}); 
