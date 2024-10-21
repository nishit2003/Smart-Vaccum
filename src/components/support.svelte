<script>
  import { Modal, Button } from "flowbite-svelte";
  export let showSupportModal = false;

  // Support FAQs
  let faqs = [
    {
      question: "How do I reset my vacuum?",
      answer: "To reset your vacuum, press and hold the power button for 10 seconds until you hear a beep. This will restore the factory settings."
    },
    {
      question: "What should I do if my vacuum is not charging?",
      answer: "Ensure that the charging dock is plugged in and that the vacuum's charging contacts are clean. You can wipe them with a dry cloth."
    },
    {
      question: "How do I clean the filters?",
      answer: "Remove the filter from the vacuum, rinse it under cold water, and let it air dry for at least 24 hours before reinstalling."
    },
    {
      question: "Why is my vacuum not picking up debris?",
      answer: "Check if the dustbin is full or if the brush roller is tangled with hair or debris. Clean these components regularly for optimal performance."
    },
    {
      question: "How do I update the firmware?",
      answer: "Connect your vacuum to the app via Wi-Fi. Navigate to the settings and check for firmware updates. Follow the on-screen instructions to update."
    }
  ];
</script>

<!-- Modal for support options -->
<Modal open={showSupportModal} on:close={() => (showSupportModal = false)} placement="center">
  <div class="modal-content">
    <h2 class="support-title">Support Options</h2>
    <div class="faq-list">
      {#each faqs as faq}
        <div class="faq-item">
          <h3 class="faq-question">{faq.question}</h3>
          <p class="faq-answer">{faq.answer}</p>
        </div>
      {/each}
    </div>
  </div>
</Modal>

<style>
  .modal-content {
    /* padding: 1.5rem;
    text-align: left; */
    padding: 2rem;
    text-align: center;
    background: linear-gradient(145deg, #e6324b, #e6324b);
    border-radius: 20px;  }
  .support-title {
    /* font-weight: bold;
    margin-bottom: 1rem; */
    font-size: 2rem;
    color: #2b2b2b;
    font-weight: bold;
    margin-bottom: 1rem;
  }
  .faq-list {
    /* margin-bottom: 2rem; */
    list-style-type: none;
    color: #2b2b2b;
    padding: 0;
    margin: 0;
    margin-bottom: 1.5rem;
  }
  .faq-item {
    /* margin-bottom: 1rem; */
    font-size: 1.1rem;
    margin-bottom: 0.7rem;
    padding: 0.7rem;
    background: #ffc6a5;
    border-radius: 10px;
    transition: transform 0.3s;
  }

  .faq-item:hover {
    transform: translateY(-3px);
  }

  .faq-question {
    text-align: left;
    font-weight: bold;
    font-family: Georgia, 'Times New Roman', Times, serif;
  }
  .faq-answer {
    text-align: left;
    font-family: Georgia, 'Times New Roman', Times, serif;
    margin-top: 0.5rem;
  }
</style>
