<template>
  <form name="contact" method="POST" data-netlify="true" :action="successRoute"
    enctype="application/x-www-form-urlencoded" netlify-honeypot="bot-field" data-netlify-recaptcha="true"
    :class="hasError ? 'has-error' : 'no-error'">
    <input type="hidden" name="form-name" value="contact" />

    <div class="form-group">
      <div class="flex-col">
        <label for="name">Name *</label>
        <input type="text" name="name" placeholder="Your chosen name" v-model="nameInput"
          :class="isNameValid ? 'is-valid' : 'is-not-valid'" />
        <div v-if="!isNameValid">
          <p class="error">Please include your name.</p>
        </div>
      </div>
      <div class="flex-col">
        <label for="email">Email Address *</label>
        <input type="text" name="email" placeholder="Your Email" :class="isEmailValid ? 'is-valid' : 'is-not-valid'"
          v-model="emailInput" />
        <div v-if="!isEmailValid">
          <p class="error">Please include your email.</p>
        </div>
      </div>
      <div class="visually-hidden">
        <label>Don’t fill this out if you’re human:</label>
        <input name="bot-field" />
      </div>
    </div>

    <div class="form-group">
      <div class="flex-col">
        <label for="message">Message *</label>
        <textarea name="message" id="message" v-model="messageInput"
          :class="isMessageValid ? 'is-valid' : 'is-not-valid'" />
        <div v-if="!isMessageValid">
          <p class="error">Please include a message.</p>
        </div>
      </div>
    </div>

    <div class="form-group text-center" @click="onSubmitClick">
      <div class="flex-col">
        <div class="flex-row align-center mb-24">
          <div data-netlify-recaptcha="true"></div>
        </div>

        <button :disabled="!isFormValid" class="btn-fill" type="submit">
          <span>Submit</span>
        </button>
      </div>

    </div>
    <div v-if="hasError" class="form-group error-group flex-col text-wrapper text-center">
      <div v-if="!isNameValid">
        <p>Please include your name.</p>
      </div>
      <div v-if="!isEmailValid">
        <p>Please include a valid email containing @.</p>
      </div>
      <div v-if="!isMessageValid">
        <p>Please include a message.</p>
      </div>
    </div>
  </form>
</template>
  
<script>
import { profanity } from '@2toad/profanity';
profanity.addWords([,"a55",
,"a55hole",
,"aeolus",
,"ahole",
,"anal",
,"analprobe",
,"anilingus",
,"anus",
,"areola",
,"areole",
,"arian",
,"aryan",
,"ass",
,"assbang",
,"assbanged",
,"assbangs",
,"asses",
,"assfuck",
,"assfucker",
,"assh0le",
,"asshat",
,"assho1e",
,"ass hole",
,"assholes",
,"assmaster",
,"assmunch",
,"asswipe",
,"asswipes",
,"azazel",
,"azz",
,"b1tch",
,"babe",
,"babes",
,"ballsack",
,"bang",
,"banger",
,"barf",
,"bastard",
,"bastards",
,"bawdy",
,"beaner",
,"beardedclam",
,"beastiality",
,"beatch",
,"beater",
,"beaver",
,"beer",
,"beeyotch",
,"beotch",
,"biatch",
,"bigtits",
,"big tits",
,"bimbo",
,"bitch",
,"bitched",
,"bitches",
,"bitchy",
,"blow job",
,"blow",
,"blowjob",
,"blowjobs",
,"bod",
,"bodily",
,"boink",
,"bollock",
,"bollocks",
,"bollok",
,"bone",
,"boned",
,"boner",
,"boners",
,"bong",
,"boob",
,"boobies",
,"boobs",
,"booby",
,"booger",
,"bookie",
,"bootee",
,"bootie",
,"booty",
,"booze",
,"boozer",
,"boozy",
,"bosom",
,"bosomy",
,"bowel",
,"bowels",
,"bra",
,"brassiere",
,"breast",
,"breasts",
,"bugger",
,"bukkake",
,"bullshit",
,"bull shit",
,"bullshits",
,"bullshitted",
,"bullturds",
,"bung",
,"busty",
,"butt",
,"butt fuck",
,"buttfuck",
,"buttfucker",
,"buttfucker",
,"buttplug",
,"c.0.c.k",
,"c.o.c.k.",
,"c.u.n.t",
,"c0ck",
,"c-0-c-k",
,"caca",
,"cahone",
,"cameltoe",
,"carpetmuncher",
,"cawk",
,"cervix",
,"chinc",
,"chincs",
,"chink",
,"chink",
,"chode",
,"chodes",
,"cl1t",
,"climax",
,"clit",
,"clitoris",
,"clitorus",
,"clits",
,"clitty",
,"cocain",
,"cocaine",
,"cock",
,"c-o-c-k",
,"cockblock",
,"cockholster",
,"cockknocker",
,"cocks",
,"cocksmoker",
,"cocksucker",
,"cock sucker",
,"coital",
,"commie",
,"condom",
,"coon",
,"coons",
,"corksucker",
,"crabs",
,"crack",
,"cracker",
,"crackwhore",
,"crap",
,"crappy",
,"cum",
,"cummin",
,"cumming",
,"cumshot",
,"cumshots",
,"cumslut",
,"cumstain",
,"cunilingus",
,"cunnilingus",
,"cunny",
,"cunt",
,"cunt",
,"c-u-n-t",
,"cuntface",
,"cunthunter",
,"cuntlick",
,"cuntlicker",
,"cunts",
,"d0ng",
,"d0uch3",
,"d0uche",
,"d1ck",
,"d1ld0",
,"d1ldo",
,"dago",
,"dagos",
,"dammit",
,"damn",
,"damned",
,"damnit",
,"dawgie-style",
,"dick",
,"dickbag",
,"dickdipper",
,"dickface",
,"dickflipper",
,"dickhead",
,"dickheads",
,"dickish",
,"dick-ish",
,"dickripper",
,"dicksipper",
,"dickweed",
,"dickwhipper",
,"dickzipper",
,"diddle",
,"dike",
,"dildo",
,"dildos",
,"diligaf",
,"dillweed",
,"dimwit",
,"dingle",
,"dipship",
,"doggie-style",
,"doggy-style",
,"dong",
,"doofus",
,"doosh",
,"dopey",
,"douch3",
,"douche",
,"douchebag",
,"douchebags",
,"douchey",
,"drunk",
,"dumass",
,"dumbass",
,"dumbasses",
,"dummy",
,"dyke",
,"dykes",
,"ejaculate",
,"enlargement",
,"erect",
,"erection",
,"erotic",
,"essohbee",
,"extacy",
,"extasy",
,"f.u.c.k",
,"fack",
,"fag",
,"fagg",
,"fagged",
,"faggit",
,"faggot",
,"fagot",
,"fags",
,"faig",
,"faigt",
,"fannybandit",
,"fart",
,"fartknocker",
,"fat",
,"felch",
,"felcher",
,"felching",
,"fellate",
,"fellatio",
,"feltch",
,"feltcher",
,"fisted",
,"fisting",
,"fisty",
,"floozy",
,"foad",
,"fondle",
,"foobar",
,"foreskin",
,"freex",
,"frigg",
,"frigga",
,"fubar",
,"fuck",
,"f-u-c-k",
,"fuckass",
,"fucked",
,"fucked",
,"fucker",
,"fuckface",
,"fuckin",
,"fucking",
,"fucknugget",
,"fucknut",
,"fuckoff",
,"fucks",
,"fucktard",
,"fuck-tard",
,"fuckup",
,"fuckwad",
,"fuckwit",
,"fudgepacker",
,"fuk",
,"fvck",
,"fxck",
,"gae",
,"gai",
,"ganja",
,"gay",
,"gays",
,"gey",
,"gfy",
,"ghay",
,"ghey",
,"gigolo",
,"glans",
,"goatse",
,"godamn",
,"godamnit",
,"goddam",
,"goddammit",
,"goddamn",
,"goldenshower",
,"gonad",
,"gonads",
,"gook",
,"gooks",
,"gringo",
,"gspot",
,"g-spot",
,"gtfo",
,"guido",
,"h0m0",
,"h0mo",
,"handjob",
,"hard on",
,"he11",
,"hebe",
,"heeb",
,"hell",
,"hemp",
,"heroin",
,"herp",
,"herpes",
,"herpy",
,"hitler",
,"hiv",
,"hobag",
,"hom0",
,"homey",
,"homo",
,"homoey",
,"honky",
,"hooch",
,"hookah",
,"hooker",
,"hoor",
,"hootch",
,"hooter",
,"hooters",
,"horny",
,"hump",
,"humped",
,"humping",
,"hussy",
,"hymen",
,"inbred",
,"incest",
,"injun",
,"j3rk0ff",
,"jackass",
,"jackhole",
,"jackoff",
,"jap",
,"japs",
,"jerk",
,"jerk0ff",
,"jerked",
,"jerkoff",
,"jism",
,"jiz",
,"jizm",
,"jizz",
,"jizzed",
,"junkie",
,"junky",
,"kike",
,"kikes",
,"kill",
,"kinky",
,"kkk",
,"klan",
,"knobend",
,"kooch",
,"kooches",
,"kootch",
,"kraut",
,"kyke",
,"labia",
,"lech",
,"leper",
,"lesbians",
,"lesbo",
,"lesbos",
,"lez",
,"lezbian",
,"lezbians",
,"lezbo",
,"lezbos",
,"lezzie",
,"lezzies",
,"lezzy",
,"lmao",
,"lmfao",
,"loin",
,"loins",
,"lube",
,"lusty",
,"mams",
,"massa",
,"masterbate",
,"masterbating",
,"masterbation",
,"masturbate",
,"masturbating",
,"masturbation",
,"maxi",
,"menses",
,"menstruate",
,"menstruation",
,"meth",
,"m-fucking",
,"mofo",
,"molest",
,"moolie",
,"moron",
,"motherfucka",
,"motherfucker",
,"motherfucking",
,"mtherfucker",
,"mthrfucker",
,"mthrfucking",
,"muff",
,"muffdiver",
,"murder",
,"muthafuckaz",
,"muthafucker",
,"mutherfucker",
,"mutherfucking",
,"muthrfucking",
,"nad",
,"nads",
,"naked",
,"napalm",
,"nappy",
,"nazi",
,"nazism",
,"negro",
,"nigga",
,"niggah",
,"niggas",
,"niggaz",
,"nigger",
,"nigger",
,"niggers",
,"niggle",
,"niglet",
,"nimrod",
,"ninny",
,"nipple",
,"nooky",
,"nympho",
,"opiate",
,"opium",
,"oral",
,"orally",
,"organ",
,"orgasm",
,"orgasmic",
,"orgies",
,"orgy",
,"ovary",
,"ovum",
,"ovums",
,"p.u.s.s.y.",
,"paddy",
,"paki",
,"pantie",
,"panties",
,"panty",
,"pastie",
,"pasty",
,"pcp",
,"pecker",
,"pedo",
,"pedophile",
,"pedophilia",
,"pedophiliac",
,"pee",
,"peepee",
,"penetrate",
,"penetration",
,"penial",
,"penile",
,"penis",
,"perversion",
,"peyote",
,"phalli",
,"phallic",
,"phuck",
,"pillowbiter",
,"pimp",
,"pinko",
,"piss",
,"pissed",
,"pissoff",
,"piss-off",
,"pms",
,"polack",
,"pollock",
,"poon",
,"poontang",
,"porn",
,"porno",
,"pornography",
,"pot",
,"potty",
,"prick",
,"prig",
,"prostitute",
,"prude",
,"pube",
,"pubic",
,"pubis",
,"punkass",
,"punky",
,"puss",
,"pussies",
,"pussy",
,"pussypounder",
,"puto",
,"queaf",
,"queef",
,"queef",
,"queer",
,"queero",
,"queers",
,"quicky",
,"quim",
,"racy",
,"rape",
,"raped",
,"raper",
,"rapist",
,"raunch",
,"rectal",
,"rectum",
,"rectus",
,"reefer",
,"reetard",
,"reich",
,"retard",
,"retarded",
,"revue",
,"rimjob",
,"ritard",
,"rtard",
,"r-tard",
,"rum",
,"rump",
,"rumprammer",
,"ruski",
,"s.h.i.t.",
,"s.o.b.",
,"s0b",
,"sadism",
,"sadist",
,"scag",
,"scantily",
,"schizo",
,"schlong",
,"screw",
,"screwed",
,"scrog",
,"scrot",
,"scrote",
,"scrotum",
,"scrud",
,"scum",
,"seaman",
,"seamen",
,"seduce",
,"semen",
,"sex",
,"sexual",
,"sh1t",
,"s-h-1-t",
,"shamedame",
,"shit",
,"s-h-i-t",
,"shite",
,"shiteater",
,"shitface",
,"shithead",
,"shithole",
,"shithouse",
,"shits",
,"shitt",
,"shitted",
,"shitter",
,"shitty",
,"shiz",
,"sissy",
,"skag",
,"skank",
,"slave",
,"sleaze",
,"sleazy",
,"slut",
,"slutdumper",
,"slutkiss",
,"sluts",
,"smegma",
,"smut",
,"smutty",
,"snatch",
,"sniper",
,"snuff",
,"s-o-b",
,"sodom",
,"souse",
,"soused",
,"sperm",
,"spic",
,"spick",
,"spik",
,"spiks",
,"spooge",
,"spunk",
,"steamy",
,"stfu",
,"stiffy",
,"stoned",
,"strip",
,"stroke",
,"stupid",
,"suck",
,"sucked",
,"sucking",
,"sumofabiatch",
,"t1t",
,"tampon",
,"tard",
,"tawdry",
,"teabagging",
,"teat",
,"terd",
,"teste",
,"testee",
,"testes",
,"testicle",
,"testis",
,"thrust",
,"thug",
,"tinkle",
,"tit",
,"titfuck",
,"titi",
,"tits",
,"tittiefucker",
,"titties",
,"titty",
,"tittyfuck",
,"tittyfucker",
,"toke",
,"toots",
,"tramp",
,"transsexual",
,"trashy",
,"tubgirl",
,"turd",
,"tush",
,"twat",
,"twats",
,"ugly",
,"undies",
,"unwed",
,"urinal",
,"urine",
,"uterus",
,"uzi",
,"vag",
,"vagina",
,"valium",
,"viagra",
,"virgin",
,"vixen",
,"vodka",
,"vomit",
,"voyeur",
,"vulgar",
,"vulva",
,"wad",
,"wang",
,"wank",
,"wanker",
,"wazoo",
,"wedgie",
,"weed",
,"weenie",
,"weewee",
,"weiner",
,"weirdo",
,"wench",
,"wetback",
,"wh0re",
,"wh0reface",
,"whitey",
,"whiz",
,"whoralicious",
,"whore",
,"whorealicious",
,"whored",
,"whoreface",
,"whorehopper",
,"whorehouse",
,"whores",
,"whoring",
,"wigger",
,"womb",
,"woody",
,"wop",
,"wtf",
,"x-rated",
,"xxx",
,"yeasty",
,"yobbo",
,"zoophile"
]);

export default {
  props: {
    successRoute: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      emailInput: null,
      nameInput: null,
      messageInput: null,
      hasError: false,
      clickedSubmit: false,
    };
  },
  computed: {
    isNameValid() {
      if (!this.clickedSubmit) {
        return "TBD";
      }
      if (!this.nameInput) {
        return false;
      }
      if (this.nameInput.length > 0) {
        return true;
      } else {
        return false;
      }
    },
    isEmailValid() {
      if (!this.clickedSubmit) {
        return "TBD";
      }
      if (!this.emailInput) {
        return false;
      }
      if (this.validateEmail(this.emailInput)) {
        return true;
      } else {
        return false;
      }
    },
    isMessageValid() {
      if (!this.clickedSubmit) {
        return "TBD";
      }
      if (!this.messageInput) {
        return false;
      }
      if (this.messageInput.length > 0) {
        return true;
      } else {
        return false;
      }
    },
    areFieldsValid() {
      return {
        name: this.isNameValid,
        email: this.isEmailValid,
        message: this.isMessageValid,
        content: !profanity.exists(this.messageInput)
      };
    },
    isFormValid() {
      if (!this.areFieldsValid) {
        return null;
      }
        const values = Object.values(this.areFieldsValid);
        if (values.includes(false)) {
          return false;
        } else {
          return true;
        }
    },
  },
  methods: {
    onSubmitClick() {
      // console.log('hi')
      this.clickedSubmit = true;
      if (!this.isFormValid) {
        this.hasError = true;
      }
      if (profanity.exists(this.messageInput)) {
        this.hasError = true;
      }
    },
    validateEmail(input) {
      const validation = input.includes("@");
      if (validation) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>


<style lang="scss" scoped>
form {
  margin-top: 64px;

  .form-group {
    display: flex;

    @media (max-width: 500px) {
      flex-direction: column;

      >*:not(:last-child) {
        margin-bottom: 24px;
      }
    }

    .flex-col {
      flex: 1;

      &:not(:last-child) {
        padding-right: 24px;
      }

      >*:not(:last-child) {
        margin-bottom: 8px;
      }
    }

    &+.form-group {
      margin-top: 40px;
    }
  }

  label {
    @include textStyle;
  }

  input[type="radio"]+label {
    @include inputStyle;
  }

  textarea {
    border: 1px solid black;
    width: 100%;
    min-height: 160px;
    padding: 4px 8px;
  }

  .container {
    display: block;
    position: relative;
    padding-left: 35px;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }

  label.container {
    @include inputStyle;
  }

  /* Hide the browser's default checkbox */
  .container input {
    position: absolute;
    opacity: 0;
    cursor: pointer;
    height: 0;
    width: 0;
  }

  .options {
    columns: 2;

    >* {
      margin-bottom: 8px;
    }
  }

  /* Create a custom checkbox */
  .checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 24px;
    width: 24px;
    background-color: transparent;
    transition: 0.3s ease all;
    border: 1px solid $golden;
  }

  /* On mouse-over, add a grey background color */
  .container:hover input~.checkmark {
    background-color: $golden;
  }

  /* When the checkbox is checked, add a blue background */
  .container input:checked~.checkmark {
    background-color: $golden;
  }

  /* Create the checkmark/indicator (hidden when not checked) */
  .checkmark:after {
    content: "";
    position: absolute;
    display: none;
  }

  /* Show the checkmark when checked */
  .container input:checked~.checkmark:after {
    display: block;
  }

  button[type="submit"] {
    min-width: 180px;
    text-align: center;
    margin-left: auto;
    margin-right: auto;
  }

  .is-not-valid {
    border-color: #fb4911;
  }

  p.error {
    color: #fb4911;
  }
}
</style>