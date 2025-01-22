<body>
<div class="container">

<div class="form-step-column">
<ul>
<li class="step">
    <div class="number-icon">1</div>
    <div>
    <span class="step-name">step 1</span> <br>
    <span class="info-name">your info</span>   
    </div>
</li>


<li class="step"> 
    <div class="number-icon">2</div>
    <div>
    <span class="step-name">step 2</span> <br>
    <span class="info-name">select plan</span>   
    </div>
</li>


<li class="step"> 
    <div class="number-icon">3</div>
    <div>
    <span class="step-name">step 3</span> <br>
    <span class="info-name">addons</span>   
    </div>
</li>



<li class="step"> 
    <div class="number-icon">4</div>
    <div>
    <span class="step-name">step 4</span> <br>
    <span class="info-name">summary</span>   
    </div>
</li>
</ul>    
</div>  
<div class="main-content"> 

<h1>Personal info</h1>

<span>Please provide your name, email address, and phone number</span>



<label for="name">Name</label>
<input type="text" placeholder="
e.g. Stephen King" name="name">

<label for="email">Email Address</label>
<input type="text" placeholder="e.g. stephenking@lorem.com">

<label for="phone">Phone Number</label>
<input type="text" placeholder="e.g. +1 234 567 890">

<button>Next Step</button>
 



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

.container{
    max-width: 80rem;
    padding: 1rem 2rem;
    background-color: var(--neutral-white);
    border-radius: 15px;
    display: flex;
    gap: 1rem;
}

.number-icon{
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
}

.step-name{
    font-variant: small-caps;
    font-size: 0.75rem;
    color: var(--neutral-white);
    color: var(--neutral-gray-1);
    text-transform: uppercase;
}

.info-name{
    font-variant: small-caps;
    color: var(--neutral-white);
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.number-icon .active{


}

.form-step-column{
  background-color: var(--primary-blue-2);
  padding: 3rem;
  border-radius: 15px;
  background-image: url('images/bg-sidebar-desktop.svg');
  background-repeat: no-repeat;
  background-size: cover;
}

.step{
    display: flex;
    gap: 0.25rem;
    align-items: center;
}

.step > *+*{
    margin: 1rem;
}

</style>