<script lang="ts">
let monthly:boolean = false;
</script>




<body>
<div class="form">
<div class="form__navbar">
<ul>
<li class="form__step-indicator">
    <div class="form__step-icon--active">1</div>
    <div>
    <span class="form__step-num">step 1</span> <br>
    <span class="form__step-name">your info</span>   
    </div>
</li>
<li class="form__step-indicator"> 
    <div class="form__step-icon">2</div>
    <div>
    <span class="form__step-num">step 2</span> <br>
    <span class="form__step-name">select plan</span>   
    </div>
</li>

<li class="form__step-indicator"> 
    <div class="form__step-icon">3</div>
    <div>
    <span class="form__step-num">step 3</span> <br>
    <span class="form__step-name">addons</span>   
    </div>
</li>

<li class="form__step-indicator"> 
    <div class="form__step-icon">4</div>
    <div>
    <span class="form__step-num">step 4</span> <br>
    <span class="form__step-name">summary</span>   
    </div>
</li>
</ul>    
</div>  
<div class="form__content"> 
<!-- <div class="form__personal-info">
<h1 class="form__header">Personal info</h1>
<span="form__description">Please provide your name, email address, and phone number</span>
<br>

<div>
<label for="name">Name</label>
<input type="text" placeholder="
e.g. Stephen King" name="name" class="form__input">
</div>

<div>
<label for="email">Email Address</label>
<input type="text" placeholder="e.g. stephenking@lorem.com" class="form__input">
</div>

<div>
<label for="phone">Phone Number</label>
<input type="text" placeholder="e.g. +1 234 567 890" class="form__input">
</div>
</div> -->

<div class="select-plan">
<h1 class="form__header">Select your plan</h1> 
<span class="form__description">You have the option of monthly or yearly billing.</span>
<div class="form__plans">
<div class="plan">
  <img src="images/icon-arcade.svg" alt="" />

  <div class="plan__description">
  <div class="plan__name">Arcade</div>
  <div class="plan__price">$9/mo</div>
  <div class="plan__deal">2 months free</div>
  </div>
</div>
 
<div class="plan">
  <img src="images/icon-advanced.svg" alt="" />
 
 <div class="plan__description">
 <div class="plan__name">Advanced</div> 
 <div class=plan__price>$12/mo</div>  
 <div class=plan__deal>2 months free</div>
 </div>
</div>
 
<div class="plan">
<img src="images/icon-pro.svg" alt="" />
  
  <div class="plan__description">
  <div class="plan__name">Pro</div> 
  <div class="plan__price">$15/mo</div> 
  <div class="plan__deal">2 months free</div>  
  </div>
</div>
</div>


<div class="form__time">
Monthly   
<label class="form__toggle">
  <input type="checkbox">
  <span class="form__slider"></span>
</label>
Yearly
</div>
</div>

<button class="go-back">Go Back</button>
<button class="step-button">Next Step</button>
</div>


</div>
</body>


<style>

:global(body) {
    background-color: var(--primary-blue-4);
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 16px;
}

.form{
    max-width: 80rem;
    padding: 1rem 2rem;
    background-color: var(--neutral-white);
    border-radius: 15px;
    display: flex;
    gap: 1rem;
    min-height: 600px;
}

.form__step-icon, .form__step-icon--active{
    background-color: var(--primary-blue-2);
    border-radius: 50%;
    border: var(--neutral-white) solid 2px;
    height: 2.2rem;
    width: 2.2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    color: var(--neutral-white);
    font-weight: bold;
    flex-shrink: 0;
}

.form__step-icon--active{
 background-color: var(--primary-blue-4);
 color: var(--primary-blue-1);
 border-color: var(--primary-blue-4);
}


.form__step-num{
    font-variant: small-caps;
    font-size: 0.75rem;
    color: var(--neutral-white);
    color: var(--neutral-gray-1);
    text-transform: uppercase;
}

.form__step-name{
    font-variant: small-caps;
    color: var(--neutral-white);
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.form__content{
    padding: 2rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;

}

.form__navbar{
  background-color: var(--primary-blue-2);
  padding: 3rem;
  border-radius: 15px;
  background-image: url('images/bg-sidebar-desktop.svg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center bottom;
}

.form__step-indicator{
    display: flex;
    gap: 0.25rem;
    align-items: center;
}

.form__step-indicator > *+*{
    margin: 1rem;
}

.step-button{
    background-color: var(--primary-blue-1);
    color: var(--neutral-white);
    padding: 1rem 1.5rem;
    border-radius: 10px;
    border: none;
    font-size: 1.1rem;
    font-weight: 500;
    align-self: self-end;
}

.step-button:hover{
    cursor:pointer;
}

.form__input{
 padding: 1rem;
 width: 100%;
 border-radius: 5px;
 outline: none;
 border: solid var(--neutral-gray-2) 1px;
 font-weight: bold;
}

.form__input::placeholder{
    color: var(--neutral-gray-1);
    font-weight: bold;
}

.personal-info > *+*{
    margin: 1rem;
}

.form__plans{

    display: flex;
    gap: 1rem;

}

.plan{

    border: solid var(--primary-blue-1) 1px;
    padding: 1rem;
    border-radius: 5px;
    cursor:pointer;
    display: flex;
    flex-direction: column;
    align-items: start;
    min-height: 200px;
}

.plan__description{
    
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
    margin-top: auto;
}

.plan__name{
  font-size: 1.2rem;
  font-weight: 400;

}

.plan__price{

 font-weight: 500;
 color: var(--neutral-gray-1);
}

.plan__deal{
 font-weight: 500;

}

.form__time
{
    background-color: var(--neutral-gray-2);
    padding: 1rem;
    text-align: center; 
}
.form__toggle{
    cursor:pointer;

}

.form__toggle > input{
    display: none;
}

.form__slider, .form__slider--toggled{
    width: 2.5rem;
    height: 1.4rem;
    background: orange;
    display: inline-block;
    border-radius: 30%;
    position: relative;
    margin: 0 1rem;
    background-color: var(--primary-blue-1);
}

.form__slider::after, .form__slider--toggled::after{
    content:'';
    position: absolute;
    width: 1rem;
    height: 1rem;
    background-color: aliceblue;
    border-radius: 50%;
    top: 50%;
    transform: translateY(-50%);
    transition: all 0.2s;
}


.form__slider--toggled::after{
    right: 50%;
}


</style>