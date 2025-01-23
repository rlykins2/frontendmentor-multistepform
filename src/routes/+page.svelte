<body>
<div class="form">
<div class="form__navbar">
<ul>
<li class="form__step-indicator">
    <div class="form__step-icon">1</div>
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
<!-- <div class="personal-info">
<h1>Personal info</h1>
<span>Please provide your name, email address, and phone number</span>

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



</div>




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
}

.form__step-icon{
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

.number-icon .active{


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


</style>