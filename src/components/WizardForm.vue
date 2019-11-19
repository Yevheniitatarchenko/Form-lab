<template>
  <div class="form-wizard">
    <ul>
      <li><a href="#">1</a></li>
      <li><a href="#">2</a></li>
      <li><a class="wizard_active" href="#">3</a></li>
    </ul>
  </div>
</template>

<style lang="scss">

h1 {
  color: #fff;
  text-align: center;
  font-size: 40px;
  line-height: 64px;
}

.form-wizard {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  margin-bottom: 51px;
  ul {
    padding: 0;
    margin: 0;
    list-style: none;
    display: flex;
    justify-content: center;
    li {
      a {
        display: inline-block;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        background: #1E34A5;
        font-size: 18px;
        color: #fff;
        text-align: center;
        line-height: 30px;
        text-decoration: none;
        margin-right: 202px;
        position: relative;
        &:before {
          content: "";
          width: 184px;
          height: 2px;
          background: #E8E8E8;
          opacity: 0.2;
          border-radius: 8px;
          position: absolute;
          right: 38px;
          top: 15px;
        }
      }
      &:last-child {
        a {
          margin-right: 0;
        }
      }
      &:first-child {
        a {
          &:before {
            display: none;
          }
            
        }
      }
    }
  }
}

.wizard_active {
  background: #DA3F5B!important;
}

@media all and (max-width: 720) {
  .wrapper {
    padding: 17px 40px 32px 40px;
  }  
}

@media all and (max-width: 600px) {
  .form-wizard {
    ul {
      li {
        a {
          margin-right: 138px;
          &:before {
            width: 120px;
          }
        }
      }
    }
  }   
}

@media all and (max-width: 480px) {
  .form-wizard {
    ul {
      li {
        a {
          margin-right: 90px;
          &:before {
            width: 74px;
          }
        }
      }
    }
  }   
}

@media all and (max-width: 370px) {
  .form-wizard {
    ul {
      li {
        a {
          margin-right: 65px;
          &:before {
            width: 50px;
          }
        }
      }
    }
  }   
}

</style>
