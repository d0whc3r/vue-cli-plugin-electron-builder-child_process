<template>
    <div class="home">
        <!--<img alt="Vue logo" src="../assets/logo.png">-->
        <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
        <button @click="testExec">exec</button>
        <button @click="testSpawn">spawn</button>
        <p>{{ result }}</p>
    </div>
</template>

<script>
  import { exec, spawn } from 'child_process';
  // @ is an alias to /src
  // import HelloWorld from '@/components/HelloWorld.vue';

  export default {
    name: 'home',
    data() {
      return {
        result: 'waiting for execute...',
      };
    },
    // components: {
    //   HelloWorld,
    // },
    methods: {
      testExec() {
        this.result = exec('echo exec success!');
      },
      testSpawn() {
        const ls = spawn('echo', ['spawn', 'success!']);

        ls.stdout.on('data', (data) => {
          console.log(`SPAWN: stdout: ${data}`);
          this.result = data;
        });

        ls.stderr.on('data', (data) => {
          console.log(`SPAWN: stderr: ${data}`);
        });

        ls.on('close', (code) => {
          console.log(`SPAWN: child process exited with code ${code}`);
        });
      }
    },
  };
</script>
