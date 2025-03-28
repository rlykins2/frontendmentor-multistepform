<script lang="ts">
import {fade} from 'svelte/transition';
let toggled:boolean = false;
let step:number = 4;
let chosen_plan:string = "arcade";
let chosen_addons:Array<string> = []; 

type Addon = {
  name: string;
  description: string;
  monthly_price: number;
  yearly_price: number;
};

type Addons = {
  [key in "online-service" | "custom-profile" | "larger-storage"]: Addon;
};

const addons:Addons = {
["online-service"]:{name:"Online Service", description:"Access to multiplayer games", monthly_price: 1, yearly_price:10}, 
["custom-profile"]:{name:"Custom Profile", description:"Custom theme on your profile", monthly_price: 2, yearly_price:20}, 
["larger-storage"]:{name:"Larger Storage", description:"Extra 1TB of cloud save", monthly_price: 2, yearly_price:20}
};

type Plan = {
  name: string;
  monthly_price: number;
  yearly_price: number;
}

type Plans = {
  [key in "advanced" | "arcade" | "pro"] : Plan;
}

const plans:Plans = {
["advanced"]: {name:"Advanced", monthly_price:9,  yearly_price:90},
["arcade"]:   {name: "Arcade",  monthly_price:12, yearly_price:120},
["pro"]:      {name: "Pro",     monthly_price:15, yearly_price:150}
};

$: total = toggled ?  plans[chosen_plan].yearly_price + chosen_addons.reduce((a,b) => a + addons[b].yearly_price, 0) : plans[chosen_plan].monthly_price
+ chosen_addons.reduce((a,b)=> a + addons[b].monthly_price, 0);


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

{#each Object.keys(plans) as plan}
<label class="plan {chosen_plan === plan ? "active" : ""}">
  <img src="images/icon-{plan}.svg" alt="" />
  <input type="radio" style="display:none;" value={plan} bind:group={chosen_plan}>
  <div class="plan__description">
  <div class="plan__name">{plans[plan].name}</div>
  {#if toggled}
  <div class="plan__price"> ${plans[plan].yearly_price}/yr</div>
  <div class="plan__deal">2 months free</div>
  {:else}
  <div class="plan__price">${plans[plan].monthly_price}/mo</div>
  {/if}
  </div>
</label>
{/each}
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

  <div class="form__addons">

  {#each Object.keys(addons) as addon}
  <label class="addon {chosen_addons.includes(addon) ? "active" : ""}">
   <div class="styled-check {chosen_addons.includes(addon) ? "active" : ""}">
        <img src="images/icon-checkmark.svg" alt="">
   </div> 
   <input type="checkbox" style="display:none" value={addon} bind:group={chosen_addons}>
  <div class="addon__text">
  <div class="addon__name">
    {addons[addon].name}
  </div> 
  <div class="addon__description">
    {addons[addon].description}
  </div> 
</div>
{#if toggled}
  <div class="addon__price">
    +${addons[addon].yearly_price}/yr
  </div> 
  {:else}
  <div class="addon__price">
    +${addons[addon].monthly_price}/mo
  </div>
  {/if}
</label>
{/each}
</div>
</div>

{:else if step === 4}
<div class="summary" in:fade>
 <h1 class="form__header">
    Finishing up
 </h1>
<span class="form__description">
    Double-check everything looks OK before confirming.
</span>

  <div class="form__summary-box">
    <div>
        {plans[chosen_plan].name} ({toggled ? 'Yearly' : 'Monthly'}) <button class="form__change-button" on:click={() => {step = 2;}}>Change</button>
    </div>
    <div class="form__plan-price">
       {toggled ? `$${plans[chosen_plan].yearly_price}/yr` : `$${plans[chosen_plan].monthly_price}/mo`}
    </div>
</div>
  {#each chosen_addons as addon}
   <div class="form__addon-summary">
    <div class="form__addon-name">{addons[addon].name}</div>
    <div class="form__addon-price">{toggled ? `$${addons[addon].yearly_price}/yr` : `$${addons[addon].monthly_price}/mo`}</div> 
</div> 
  {/each}
  <div class="total"><div class="total__indicator">Total (per { toggled ? "year" : "month"})</div> <span class="total__price">+${total}/{toggled ? "yr" : "mo"}</span></div>
</div>
{:else}
  <div class="gratitude">
  <div class="gratitude__icon"> 
  <img src="images/icon-thank-you.svg" alt="">
  </div>
  <h1>Thank you!</h1>

  <p>Thanks for confirming your subscription! We hope you have fun 
  using our platform. If you ever need support, please feel free 
  to email us at support@loremgaming.com.</p>
  </div>
{/if}


<div class="button-bar">
{#if step > 1 && step < 5}
<button class="go-back-button" on:click={somethingelse}>Go Back</button>
{/if}
{#if step < 5}
<button class="step-button" on:click={something}>{step < 4 ? "Next Step" : "Confirm"}</button>
{/if}
</div>
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
    width: 50rem;
    padding: 1rem 2rem;
    background-color: var(--neutral-white);
    border-radius: 15px;
    display: flex;
    gap: 1rem;
    height: 600px;
}

.form__header{

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


.form__personal-info {
  width: 100%;
  height: 100%;
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;

}

.form__addons{
  width: 100%;
  height: 100%;
  flex-grow: 1;
}

.select-plan{
  width: 100%;
  height: 100%;
  flex-grow: 1;

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
    margin-left: auto;
}

.go-back-button{
    margin-left: 0;
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
 transition: all .2s;
}

.form__input::placeholder{
    color: var(--neutral-gray-1);
    font-weight: bold;
}

.form__input:focus{
  outline-style: solid;
  outline-color: var(--primary-blue-2);
  outline-width: 2px;
}

.personal-info > *+*{
    margin: 1rem;
}

.form__plans{

    display: flex;
    gap: 1rem;

}

.plan{

    border:  var(--neutral-gray-2) 1px solid;
    padding: 1rem;
    border-radius: 5px;
    cursor:pointer;
    display: flex;
    flex-direction: column;
    align-items: start;
    min-height: 200px;
    user-select: none;
    transition: all .2s;
    flex-grow: 1;
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
    border: 1px solid var(--neutral-gray-2);
    border-radius: 5px;
    padding: 1rem;
    cursor: pointer;
    gap: 1rem;
    user-select: none;
    transition: all .2s;
}

.addon__price{
  margin-left: auto;
}


.addon:hover{
 border: 1px solid var(--primary-blue-2);

}


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

.button-bar{
  display: flex;

}

.form__change-button{
    background: none;
    border: none;
    cursor: pointer;
    text-decoration: underline;
    color: var(--primary-blue-2);
    display: block;
}

.form__summary-box{
    padding: 1rem;
    border-radius: 5px 5px 0px 0px;
    background-color: var(--neutral-magnolia);
    border-bottom: solid 1px var(--neutral-gray-1);
    display: flex;
    align-items: center;
}

.form__plan-price{
  margin-left: auto;
  font-size: 1.3rem;
}

.form__addon-summary{
    padding: 1rem;
    background-color: var(--neutral-magnolia); 
    display: flex;
}

.form__addon-summary:last-child{
    border-radius: 0 0 5px 5px;
}
.form__addon-name{
    color: var(--neutral-gray-1);
    font-weight: 500;
    font-size: 0.9rem;
}

.form__addon-price{
    margin-left: auto;
    font-weight: 500;
    color: var(--primary-blue-1);
    font-size: 0.9rem;
}

.form__addons > *+*{ margin-top: 0.3rem;
}

.total__price{
  font-size: 2rem;
  color: var(--primary-blue-2);
  margin-left: auto;
  display: block;
  font-weight: bold;
}
.total{
  display: flex;
  align-items: center;
}

.total__indicator{
  font-weight: 500;
  color: var(--neutral-gray-1);
}

.gratitude{
  display: flex;
  flex-direction: column;
}

.gratitude__icon{
  width: 10rem;
  height: 10rem;
}

.gratitude__icon > img {
  max-width: 100%;
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