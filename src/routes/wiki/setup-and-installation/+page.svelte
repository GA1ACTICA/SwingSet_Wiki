<script>
  import VSC_Extension_Icon from "$lib/assets/setup-and-installation/VSC-extension-icon.png";
  import VSC_Extension_List from "$lib/assets/setup-and-installation/VSC-extension-list.png";
  import VSC_Create_Project from "$lib/assets/setup-and-installation/VSC-create-project.png";
  import VSC_Choose_Build_Tool from "$lib/assets/setup-and-installation/VSC-choose-build-tool.png";
</script>

<h1>Setup and Installation</h1>
<br />

<p>
  This part of the wiki will guide you through setting up a <a
    href="https://gradle.org/">Gradle</a
  > project in Visual studio code (VSC).
</p>
<br />

<p>
  If you are using another code editor some parts of this guide won't be
  applicable for you. Some extra resources for that step will be marked with a <b
    >*</b
  >. These will typically be link to external resources but can also be
  alternative solutions.
</p>
<br />

<h3>1. Getting Gradle</h3>
<p>
  Gradle is the project manager that we will be using in the wiki. It helps
  manage dependencies (like SwingSet) and tasks used for publishing, ruining the
  application and generate documentation from your code. But there is no need to
  worry if you don't know how gradle works. There is probably a big chance that
  your favorite code editor already has a good gradle plugin or extension so
  there is no need to start memorizing commands.
</p>
<br />

<section>
  <div>
    <p>
      In VSC on the bar to the left there should be a icon with four squares
    </p>

    <img src={VSC_Extension_Icon} alt="[VSC extension icon]" />

    <p>
      After pressing on the icon or pressing the key combination <b
        >Ctrl + Shift + X</b
      >
      a menu with you installed extensions should show up. In that menu you search
      for
      <b>Java</b>. You should now see this:
    </p>
    <br />

    <p>
      Choose the extension on the picture named: <br />
      <b>Extension Pack for Java</b>
    </p>
    <br />

    <p>
      This will enable you to use features like autocomplete, running the code
      directly from VSC and the ability to use gradle.
    </p>
  </div>
  <div>
    <img
      src={VSC_Extension_List}
      alt="[VSC extension list]"
      style="object-fit: contain;"
    />
  </div>
  <br />

  <p>* [Insert other methods here]</p>
</section>
<br />

<h2>2. Setting up a Gradle project</h2>
<br />

<p>
  After installing the extension we need to create the java project. <br /> You
  do this by pressing <b>Ctrl + Shift + P </b>, then writing:
  <b>"Java: Create"</b>
  and choosing the first option: <b>"&gt; Java: Create Java Project...""</b>
</p>
<img src={VSC_Create_Project} alt="[VSC create project]" />
<br />

<p>After that you choose Gradle</p>
<img src={VSC_Choose_Build_Tool} alt="[VSC choose build tool]" />
<br />

<p>
  Then you find where you want to put your project. After that you choose Groovy
  as your build script DSL and lastly you name it!
</p>
<br />

<h2>3. Importing SwingSet Engine</h2>

<style>
  section {
    display: flex;
    height: 25rem;
  }

  section * {
    flex: 1;
  }

  img {
    border-radius: 1rem;
    max-width: 100%;
    max-height: 100%;
    width: auto;
    height: auto;
    object-fit: contain;
    border: 0.1rem solid aliceblue;
    margin: 0.5rem;
  }
</style>
