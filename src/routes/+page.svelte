<script lang="ts">
import {fade} from 'svelte/transition';
let toggled:boolean = false;
let step:number = 3;
let chosen_plan:string = "";
let chosen_addons:Array<string> = []; 
const something = () => {if (step < 5) step += 1};
const somethingelse = () => {if (step > 1) step -= 1};
</script>

<div class="form">
{#if step < 5}
<div class="form__navbar">
<ul>
<li class="form__step-indicator">
    <div class="form__step-icon {step == 1? 'active': ''}">1</div>
    <div>
    <span class="form__step-num">step 1</span> <br>
    <span class="form__step-name">your info</span>   
    </div>
</li>

<li class="form__step-indicator"> 
    <div class="form__step-icon {step == 2? 'active': ''}">2</div>
    <div>
    <span class="form__step-num">step 2</span> <br>
    <span class="form__step-name">select plan</span>   
    </div>
</li>

<li class="form__step-indicator"> 
    <div class="form__step-icon {step == 3? 'active': ''}">3</div>
    <div>
    <span class="form__step-num">step 3</span> <br>
    <span class="form__step-name">addons</span>   
    </div>
</li>

<li class="form__step-indicator"> 
    <div class="form__step-icon {step == 4? 'active': ''}">4</div>
    <div>
    <span class="form__step-num">step 4</span> <br>
    <span class="form__step-name">summary</span>   
    </div>
</li>
</ul>    
</div> 
{/if}


<div class="form__content"> 

{#if step === 1}   
<div class="form__personal-info" in:fade>
<h1 class="form__header">Personal info</h1>
<span class="form__description">Please provide your name, email address, and phone number</span>
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
</div>

{:else if step === 2}
<div class="select-plan" in:fade>
<h1 class="form__header">Select your plan</h1> 
<span class="form__description">You have the option of monthly or yearly billing.</span>
<div class="form__plans">
<label class="plan {chosen_plan === "Arcade" ? "active" : ""}">
  <img src="images/icon-arcade.svg" alt="" />
  <input type="radio" style="display:none;" value="Arcade" bind:group={chosen_plan}>
  <div class="plan__description">
  <div class="plan__name">Arcade</div>
  {#if toggled}
  <div class="plan__price"> $90/yr</div>
  <div class="plan__deal">2 months free</div>
  {:else}
  <div class="plan__price">$9/mo</div>
  {/if}
  </div>
</label> 
<label class="plan {chosen_plan === "Advanced" ? "active" : ""}">
 <img src="images/icon-advanced.svg" alt="" />
 <input type="radio" style="display:none;" value="Advanced" bind:group={chosen_plan}>
 <div class="plan__description">
 <div class="plan__name">Advanced</div> 
 {#if toggled}
 <div class="plan__price"> $120/yr</div>
 <div class="plan__deal">2 months free</div>
 {:else}
 <div class="plan__price">$12/mo</div>  
 {/if}
</div>
</label>
 
<label class="plan {chosen_plan === "Pro" ? "active" : ""}">
<input type="radio" style="display:none;" value="Pro" bind:group={chosen_plan} >
<img src="images/icon-pro.svg" alt="" />
  <div class="plan__description">
  <div class="plan__name">Pro</div> 
  {#if toggled}
  <div class="plan__price"> $150/yr</div>
  <div class="plan__deal">2 months free</div>
  {:else}
  <div class="plan__price">$15/mo</div> 
  {/if}
</div>
</label>
</div>


<div class="form__time">
<span class="time__description {!toggled ? "active": ""}">Monthly</span>   


<label class="form__toggle">
  <input type="checkbox" bind:checked={toggled}>
  <span class={["form__slider", {toggled}]}></span>
</label>

<span class="time__description {toggled ? "active" : ""}">Yearly</span>
</div>
</div>


{:else if step === 3}
<div class="addons" in:fade>
 <h1 class="form__header">Pick add-ons</h1> 
  <span class="form__description">Add-ons help enhance your gaming experience</span> 
  
  <label class="addon {chosen_addons.includes("online-service") ? "active" : ""}">
   <div class="styled-check {chosen_addons.includes("online-service") ? "active" : ""}">
        <img src="images/icon-checkmark.svg" alt="">
   </div> 
   <input type="checkbox" style="display:none" value="online-service" bind:group={chosen_addons}>
  <div class="addon__text">
  <div class="addon__name">
    Online service
  </div> 
  <div class="addon__description">
    Access to multiplayer games
  </div> 
</div>
{#if toggled}
  <div class="addon__price">
    +$10/yr
  </div> 
  {:else}
  <div class="addon__price">
    +$1/mo
  </div>
  {/if}
</label>



<label class="addon {chosen_addons.includes("larger-storage") ? "active" : ""}" >
  <div class="styled-check {chosen_addons.includes("larger-storage") ? "active" : ""}">
    <img src="images/icon-checkmark.svg" alt="">
  </div> 
  <input type="checkbox" style="display:none" value="larger-storage" bind:group={chosen_addons} on:click={() => console.log(chosen_addons)}>
  <div class="addon__text">
  <div class="addon__name">
    Larger storage
  </div> 
  <div class="addon__description">
    Extra 1TB of cloud save
  </div> 


</div>
{#if toggled}
  <div class="addon__price">
    +$10/yr
  </div> 
  {:else}
  <div class="addon__price">
    +$2/mo
  </div>
  {/if}
</label>


<label class="addon {chosen_addons.includes("custom-profile") ? "active" : ""}">
<div class="styled-check {chosen_addons.includes("custom-profile") ? "active" : ""}">
    <img src="images/icon-checkmark.svg" alt="">
</div> 
<input type="checkbox" style="display:none" value="custom-profile" bind:group={chosen_addons}>
  <div class="addon__text">
  <div class="addon__name">
    Customizable Profile
  </div> 
  <div class="addon__description">
    Custom theme on your profile
  </div> 
</div>
{#if toggled}
  <div class="addon__price">
    +$10/yr
  </div> 
  {:else}
  <div class="addon__price">
    +$2/mo
  </div>
  {/if}
</label>
</div>

{:else if step === 4}
<div class="summary" in:fade></div>
{/if}

{#if step > 1 && step < 5}
<button class="go-back-button" on:click={somethingelse}>Go Back</button>
{/if}

{#if step < 5}
<button class="step-button" on:click={something}>{step < 4 ? "Next Step" : "Confirm"}</button>
{/if}
</div>
</div>

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

.form__step-icon.active{
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

.go-back-button, .step-button{
    background-color: var(--primary-blue-1);
    color: var(--neutral-white);
    padding: 1rem 1.5rem;
    border-radius: 10px;
    border: none;
    font-size: 1.1rem;
    font-weight: 500;
    align-self: self-end;
}

.go-back-button{
    align-self: self-start;
    color: var(--neutral-gray-1);
    background-color: white;
}


.step-button:hover, .go-back-button:hover{
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

    border: solid var(--neutral-gray-2) 1px;
    padding: 1rem;
    border-radius: 5px;
    cursor:pointer;
    display: flex;
    flex-direction: column;
    align-items: start;
    min-height: 200px;
    user-select: none;
    transition: all .2s;
}

.plan:hover
{
    border-color: var(--primary-blue-1);
}

.plan.active{
    border-color: var(--primary-blue-1);
    background-color: var(--neutral-magnolia);
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
    user-select: none;
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
    border-radius: 40%;
    position: relative;
    margin: 0 1rem;
    background-color: var(--primary-blue-1);
}

.form__slider::after{
    content:'';
    position: absolute;
    width: 1rem;
    height: 1rem;
    background-color: aliceblue;
    border-radius: 50%;
    top: 50%;
    transform: translate(-100%,-50%);
    transition: transform 0.2s;
}


.form__slider.toggled::after{
   transform: translate(0%, -50%); 
}

.time__description{

    color: var(--neutral-gray-1);
}

.time__description.active{
    color: var(--primary-blue-1);
}

.form__addons > *+*{
  margin-top: 2rem;
}

.addon{
    display: flex;
    align-items: center;
    border: 1px solid var(--neutral-gray-1);
    border-radius: 5px;
    padding: 1rem;
    cursor: pointer;
    gap: 1rem;
    user-select: none;
}

.addon:hover{}


.addon.active{
    border: 1px solid var(--primary-blue-2);
    background-color: var(--neutral-magnolia);
}


.styled-check{
    width: 1.2rem;
    height: 1.2rem;
    border-radius: 5px;
    border: var(--neutral-gray-1) 1px solid;
    transition: background-color 0.2s;
    background-color: white;
    position: relative;
}

.styled-check.active{
  background: var(--primary-blue-2);
}

.styled-check > img{
    position: absolute;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
}

.styled-check.active > img{


}

/* .styled-check.active::before{
    content: '';
    background-image: url("images/icon-checkmark.svg");
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
} */


</style>