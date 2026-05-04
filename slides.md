---
theme: ./local-theme
colorSchema: light
layout: cover
institute: Robotics Institute
course: 41118 AI in robotics
topic: Introduction to End-to-End Robotics
title: Introduction to End-to-End Robotics
author: Gibson Hu
info: |
  Robotics Institute - 41118 AI in Robotics - Introduction to End-to-End Robotics
drawings:
  persist: false
mdc: true
duration: 60min
addons:
  - tikzjax
download: false
css: style.css
---

---
layout: center
class: text-center
---

# Big Question

<div class="question-visual">
  <div class="big-quote">
  Can a robot learn the whole path from <span>sensing</span> to <span>acting</span>?
  </div>
  <img src="https://lh3.googleusercontent.com/hspU6wlYJlWD-KxCBjstU5_3dK7cuwyxMDhEOTWAjPBTpfnHvNXIZLdpcZi5ep3UnsfS98mIKilxb0pAWufFA6X_Ir2Q0x-Vl8dMMHsen_4GXam0%3Dw1440-h810-n-nu" alt="Robot arm manipulating objects on a table from RT-2" />
</div>

---
layout: two-cols
---

# What is Robotics?

Robotics combines sensing, reasoning, motion, and control to make machines interact with the physical world.

<div class="grid-4 compact mt-8">
  <div class="tile">👁️<br/><b>Sense</b><br/>cameras, depth, touch</div>
  <div class="tile">🧠<br/><b>Decide</b><br/>planning and policies</div>
  <div class="tile">🦾<br/><b>Act</b><br/>motors and grippers</div>
  <div class="tile">🌍<br/><b>Adapt</b><br/>messy real world</div>
</div>

::right::

<figure class="online-figure">
  <img src="https://commons.wikimedia.org/wiki/Special:FilePath/UR16e_robot_arm.png" alt="Collaborative robot arm" />
  <figcaption>Modern cobot hardware: sensors, joints, controller, and gripper.</figcaption>
</figure>

---
layout: default
---

# Traditional Robotics Pipeline

<div class="pipeline-visual modules">
  <div><span>Camera</span><b>Sensors</b></div>
  <div><span>Detect</span><b>Perception</b></div>
  <div><span>Track</span><b>State</b></div>
  <div><span>Search</span><b>Planning</b></div>
  <div><span>Servo</span><b>Control</b></div>
  <div><span>Move</span><b>Action</b></div>
</div>

<div class="note mt-8">
Traditional systems break the problem into modules. Each module is designed, tuned, and tested separately.
</div>

---
layout: default
---

# End-to-End Robotics Pipeline

<div class="e2e-visual">
  <div class="sensor-card">
    <img src="/images/obs.png" alt="Robot pushing a T-shaped block" />
    <span>observation</span>
  </div>
  <div class="network-card">
    <span></span><span></span><span></span>
    <b>learned policy</b>
  </div>
  <div class="action-card">
    <b>Δx, Δθ, gripper</b>
    <span>next action sequence</span>
  </div>
</div>

<div class="big-formula mt-8">observation + goal → neural network → action</div>

---
layout: two-cols
---

# Bimanual Manipulators

What the policy observes:

- Multi-camera views of both arms and the workspace
- Joint angles for the left and right manipulators
- Gripper state and contact-rich object motion
- Task goal, demonstration history, or language cue
- Relative pose between both end-effectors

::right::

<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://website.pi-asset.com/v2/upload/lowres_processed2xspeed_arx4_website_batch4.mp4" type="video/mp4" />
  </video>
</div>



<div class="caption mt-3">
End-to-end bimanual control learns to coordinate two arms as one policy for handoff, folding, assembly, and tool use.
</div>

Outputs can include synchronized reaches, two-handed grasps, force-aware repositioning, and smooth handover motions.

---
layout: two-cols
---

# Humanoid End-to-End Example

What the policy observes:

- Head and wrist camera video
- Joint angles and body pose
- Foot contact and balance signals
- Language instruction or task goal
- Recent actions and motion history

::right::

<div class="video-card">
  <iframe
    src="https://www.youtube.com/embed/HYwekersccY"
    title="Humanoid robotics example video"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen
  ></iframe>
</div>

<div class="caption mt-3">
Humanoid end-to-end robotics maps perception, balance, and task context directly into whole-body actions.
</div>

Outputs can include walking, reaching, grasping, gaze, and recovery motions as one coordinated policy.

---
layout: default
---

# Example Task: Pick Up a Cup

<div class="cup-task-visual" aria-label="Robot arm observing and reaching for a cup">
  <div class="robot-arm">
    <span class="joint shoulder"></span>
    <span class="link upper"></span>
    <span class="joint elbow"></span>
    <span class="link forearm"></span>
    <span class="gripper"></span>
  </div>
  <div class="tabletop">
    <span class="cup"></span>
    <span class="block red"></span>
    <span class="block blue"></span>
  </div>
  <div class="vision-box">
    <span>camera view</span>
  </div>
  <div class="action-path"></div>
</div>

<div class="sequence">
  <div>📷<br/><b>Observe</b><br/>camera sees cup</div>
  <div>🧠<br/><b>Predict</b><br/>policy chooses action</div>
  <div>🦾<br/><b>Move</b><br/>arm reaches and grasps</div>
  <div>✅<br/><b>Check</b><br/>success or retry</div>
</div>

---
layout: default
---

# Main Learning Approaches

<div class="grid-3 visual-cards mt-8">
  <div class="card"><div class="card-icon demo"></div><b>Imitation Learning</b><br/>Learn from expert demonstrations.</div>
  <div class="card"><div class="card-icon reward"></div><b>Reinforcement Learning</b><br/>Learn by trial, reward, and feedback.</div>
  <div class="card"><div class="card-icon dataset"></div><b>Offline Robot Learning</b><br/>Learn from existing datasets without new trials.</div>
</div>

---
layout: two-cols
---

# Imitation Learning

The robot copies behavior from demonstrations.



The idea is very intuitive: show the robot what to do, then train it to repeat similar behavior.

::right::

<div class="demo-loop">
  <div>Human demo</div>
  <div>Dataset</div>
  <div>Train Policy</div>
  <div>Robot Deploy</div>
</div>


---
layout: two-cols
---

# Human Demonstration

- A human teleoperates or physically guides the robot
- Cameras and joint sensors record every step
- Successful trials become training demonstrations
- The learned policy later imitates the same behavior on its own

::right::

<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://packaged-media.redd.it/5nijvjz0nzsg1/pb/m2-res_590p.mp4?m=DASHPlaylist.mpd&c=wh_ben_en&var=sgpssan&v=1&e=1777658400&s=90c814c98b8b9ce47ad03005b9eb1cc496dd7baa" type="video/mp4" />
  </video>
</div>

<div class="caption mt-3">
The key idea is simple: the robot first watches or feels an expert solve the task, then learns to reproduce that sequence.
</div>
---
layout: two-cols
---

# Dataset


- Each episode records camera views over time
- Robot states and actions are saved at each step
- Different trials capture variation in objects and motion
- The dataset becomes the training signal for the policy
- Hunderds if not thousands of human demonstration are required for a robot to perform the action successfully


::right::

<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://packaged-media.redd.it/a08moyrqeixg1/pb/m2-res_1080p.mp4?m=DASHPlaylist.mpd&var=sgpssan&v=1&e=1777658400&s=6c6f54261454c48b002b9bd66628ecd195975acb" type="video/mp4" />
  </video>
</div>

<div class="caption mt-3">
A dataset browser lets us inspect many recorded episodes, compare camera views, and see how trajectories vary across demonstrations.
</div>

---
layout: two-cols
---

# Training

- Episodes are loaded in batches from the dataset
- Neural Network is trained to predict the actions given observation
- Goal is to reduce the loss function while performing well on validation datasets

::right::

<figure class="online-figure training-figure">
  <img src="https://preview.redd.it/what-is-the-benefit-of-using-tools-such-as-weight-and-v0-s16aecu2mqcg1.png?auto=webp&s=40181e2bf342aeee070758147dc323e6410a7c82" alt="Training dashboard showing loss curves and experiment tracking" />
</figure>

<div class="caption mt-3">
During training, we watch metrics like loss and validation performance to see whether the policy is actually learning useful behavior.
</div>

---
layout: two-cols
---

# Policy Deployment


- Live camera images and robot state are streamed into the policy
- The policy predicts the next action at every control step
- Those actions are sent to the robot controller in real time
- The robot keeps observing, acting, and updating in a closed loop

::right::

<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://website.pi-asset.com/pi07/zeroshot_air_fryer_attempt_compressed.mp4" type="video/mp4" />
  </video>
</div>

<div class="caption mt-3">
Deployment means taking the trained model out of the notebook and letting it drive the physical robot from live observations.
</div>

---
layout: default
---

# Different Imitation Learning Policies

<div class="grid-4 compact mt-8">
  <div class="card"><b>Diffusion Policy</b><br/>Starts with noisy actions, then denoises into a smooth plan.</div>
  <div class="card"><b>ACT</b><br/>Predicts chunks of future actions with a transformer.</div>
  <div class="card"><b>VLA</b><br/>Vision + language + robot data → action tokens.</div>
  <div class="card"><b>Generalist Policies</b><br/>Pretrained on many robots, then adapted to a new robot.</div>
</div>

<div class="note mt-8">
All of these are Imitation Learning, but they differ in the action representation: text-like tokens, denoised trajectories, action chunks, or pretrained multi-robot policies.
</div>

<div class="project-strip mt-6">
  <figure><img src="https://diffusion-policy.cs.columbia.edu/images/teaser.svg" alt="Diffusion Policy paper teaser" /><figcaption>Diffusion Policy</figcaption></figure>
  <figure><img src="https://tonyzhaozh.github.io/aloha/resources/algo.png" alt="ACT architecture from ALOHA paper" /><figcaption>ACT</figcaption></figure>
  <figure><img src="https://openvla.github.io/static/images/openvla_model.jpg" alt="OpenVLA model figure" /><figcaption>VLA</figcaption></figure>
  <figure><img src="https://octo-models.github.io/teaser.jpg" alt="Octo project teaser" /><figcaption>Generalist</figcaption></figure>
</div>



---
layout: default
class: big-heading
---

# Diffusion Policy

<div class="diffusion-policy-overview">
  <div>
    Core idea: instead of predicting one action directly, the policy generates a short action sequence by denoising it step by step.

    - Input: camera observations and robot state
    - Output: a smooth future trajectory
    - Best at: continuous manipulation where many action paths could work
  </div>

  <figure class="project-figure diffusion-policy-figure">
    <img src="https://ar5iv.labs.arxiv.org/html/2303.04137/assets/x3.png" alt="Diffusion Policy teaser figure" />
    <figcaption>Project overview: observations condition a denoising policy over actions.</figcaption>
  </figure>
</div>

---
layout: two-cols
---

# Before Robotics: Diffusion

Diffusion models were first popularized in generative media tasks.

- In image generation, a model starts from noise and gradually denoises toward a valid image.
- Diffusion Policy borrows the same idea, but denoises an action sequence instead of pixels.
- That makes it natural for multimodal behavior: several different futures can all be valid.

::right::

<div class="origin-grid">
  <div>
    <img src="https://developer-blogs.nvidia.com/wp-content/uploads/2024/07/diffusion-model-building.gif" alt="Diffusion image generation process from noise to image" />
    <span>Image generation: noise → denoise → final image</span>
  </div>
  <div>
    <div class="video-card">
      <video autoplay muted loop playsinline controls>
        <source src="https://diffusion-policy.cs.columbia.edu/videos/highlight_pusht_process.mp4" type="video/mp4" />
      </video>
    </div>
    <span>Robot control: noise → denoise → final trajectory</span>
  </div>
</div>

---
layout: two-cols
---

# Why Diffusion Helps Manipulation

Many robot tasks are multimodal.

Example: to push an object, the robot may approach from the left or right. Both can be correct.

Diffusion policies can represent several possible futures before settling on one consistent action sequence.

::right::

<figure class="project-figure ">
  <img src="https://diffusion-policy.cs.columbia.edu/images/multimodal_sim.svg" alt="Diffusion Policy multimodal behavior figure" />
  <figcaption>Project figure: diffusion can model multiple valid action modes.</figcaption>
</figure>

---
layout: two-cols
---

# Example: Diffusion Policy

- Diffusion Policy is a visuomotor policy that treats robot control as conditional action denoising. Instead of predicting one action directly, it iteratively refines a noisy action sequence into a usable plan. [Project](https://diffusion-policy.cs.columbia.edu/) | [Paper](https://arxiv.org/abs/2303.04137)
- In the example, the model solves manipulation tasks like Push-T by generating and refining a short trajectory, then executing part of it before replanning. [Demo video](https://diffusion-policy.cs.columbia.edu/videos/pusht_ep6_diffusion.mp4)
- It is a useful example because diffusion handles multimodal robot behavior well and showed strong results across many benchmark manipulation tasks. [Project page](https://diffusion-policy.cs.columbia.edu/)

::right::

<figure class="online-figure vla-teaser-figure mb-4">
  <img src="https://diffusion-policy.cs.columbia.edu/images/teaser.svg" alt="Diffusion Policy project teaser" />
</figure>

<div class="video-card vla-teaser-video">
  <video autoplay muted loop playsinline controls>
    <source src="https://diffusion-policy.cs.columbia.edu/videos/pusht_ep6_diffusion.mp4" type="video/mp4" />
  </video>
</div>

<div class="caption">Diffusion Policy project video: denoise a Push-T action sequence.</div>

---
layout: default
class: big-heading
---


# ACT (Action Chucking Transformers)

<div class="act-overview">
  <div>
    Core idea: instead of predicting one action directly, the policy generates a short action sequence by denoising it step by step.

    - It predicts a chunk of future actions, not just the next control step.
    - It is trained from demonstrations, often teleoperated ones.
    - It works especially well for long, precise manipulation sequences.

  </div>

  
  <figure class="project-figure">
    <img src="https://tonyzhaozh.github.io/aloha/resources/algo.png" alt="ACT architecture overview" />
    <figcaption>ACT predicts short windows of future actions from multi-camera robot observations.</figcaption>
  </figure>

</div>

---
layout: two-cols
---

# Before Robotics: Transformers

Before ACT, transformers were already strong at sequence modeling.

- In language, transformers predict the next tokens in a sentence.
- In ACT, the sequence is not words but robot actions over time.
- The chunking idea helps the robot plan a short motion phrase instead of one tiny twitch.

::right::

<div class="origin-grid">
  <div>
    <img src="https://images.ctfassets.net/kftzwdyauwt9/7LzxdzMcijUYHtIES6rmub/1dd3bc9f423a6b1cd5176936dbb029aa/Entry_Point.png?w=3840&q=90&fm=webp" alt="Diffusion image generation process from noise to image" />
    <span>Language: token sequence over time</span>
  </div>
  <div>
    <div class="video-card">
      <video autoplay muted loop playsinline controls>
        <source src="https://mobile-aloha.github.io/resources/mobile-aloha.mp4" type="video/mp4" />
      </video>
    </div>
    <span>Robot control: action sequence over time</span>
  </div>
</div>


---
layout: two-cols
---

# ACT: Temporal Aggregation

Instead of predicting one tiny action at a time, ACT predicts a short future window.

```text
observation now → [a₁, a₂, a₃, ... aₖ]
```

This helps long-horizon tasks because the policy commits to a small motion plan, not just the next twitch.

ACT often predicts overlapping action chunks at every timestep.

Multiple predictions vote on what the robot should do now.

<div class="note mt-6">
Temporal aggregation smooths control and reduces jitter from individual predictions.
</div>

::right::

<figure class="project-figure">
  <img src="/images/act/temporal-aggregation.svg" alt="ACT temporal aggregation diagram with overlapping action chunks and weighted ensemble" />
  <figcaption>Temporal aggregation combines overlapping action chunk predictions into a smoother command.</figcaption>
</figure>


---
layout: two-cols
---

# Example: ACT

- ACT is the policy introduced with the ALOHA system for fine-grained bimanual manipulation. It uses a transformer to predict short chunks of future robot actions from multi-camera observations and joint state. [Project](https://tonyzhaozh.github.io/aloha/) | [Paper](https://arxiv.org/abs/2304.13705)
- In the ACT example, the robot uses teleoperated demonstrations to learn coordinated two-arm behaviors such as opening lids and handling objects in contact-rich settings. [Demo video](https://tonyzhaozh.github.io/aloha/resources/open_lid.mp4)
- It is a useful example because it shows that end-to-end imitation learning can work on low-cost hardware with relatively small amounts of task-specific data. [Project page](https://tonyzhaozh.github.io/aloha/)

::right::

<figure class="online-figure vla-teaser-figure mb-4">
  <img src="https://tonyzhaozh.github.io/aloha/resources/algo.png" alt="ACT architecture overview" />
</figure>

<div class="video-card vla-teaser-video">
  <video autoplay muted loop playsinline controls>
    <source src="https://tonyzhaozh.github.io/aloha/resources/open_lid.mp4" type="video/mp4" />
  </video>
</div>

<div class="caption">ALOHA / ACT project video: bimanual task execution.</div>

---
layout: two-cols
class: big-heading
---

# VLA Models

Vision-Language-Action models combine perception, language understanding, and action prediction in one network.

Modern end-to-end systems can combine:

<div class="big-formula mt-8">
image + instruction + robot state → action
</div>

Example instruction:

> “Pick up the red block and place it in the bowl.”

::right::

<figure class="online-figure">
  <img src="https://lh3.googleusercontent.com/wS51jyqW2T7T_m14tD2kn4pg86isQ1i7kusjlkQC-OktXdDgz-2iG4m_oZB8aFNmulk5ckURCxItJ1yWMVX54uU5k1WshHFKiqbhmNjlQmtgeN-O%3Dw1440" alt="RT-2 vision-language-action training diagram" />
  <figcaption>RT-2: VLMs adapted to output robot actions.</figcaption>
</figure>

---
layout: two-cols
---

# Before Robotics: VLMs and LLMs

VLAs come from the same family as vision-language and language models.

- VLMs learned to connect images and text.
- LLM-style transformers learned large-scale sequence prediction.
- VLAs reuse that machinery, but ask the model to output robot actions.

::right::

<div class="origin-grid">
  <div>
    <img src="/images/VLM_example.png" alt="Chatbots: Vision-language models" />
    <span>Using Images/Videos in VLM ChatBots </span>
  </div>
  <div>
    <div class="video-card">
      <video autoplay muted loop playsinline controls>
        <source src="https://openvla.github.io/static/videos/comparisons_with_baselines/rt1_robot/rt2x--move_coke_can_near_taylor_swift.mp4" type="video/mp4" />
      </video>
    </div>
    <span>Model can take Language and Vision to predict Robot actions.    (Give the coke to Tailor Swift)</span>
  </div>
</div>

<!-- <div class="origin-grid">
  <div><b>Vision-language models</b><span>image + text → text</span></div>
  <div><b>VLA models</b><span>image + text + state → action</span></div>
</div> -->

---
layout: two-cols
---

# VLA Internals: What Gets Tokenized?

VLA models turn a robot problem into a sequence prediction problem.

<div class="token-flow">
  <div><b>Image patches</b><span>visual tokens</span></div>
  <div><b>Instruction</b><span>language tokens</span></div>
  <div><b>Robot state</b><span>joint / gripper tokens</span></div>
  <div><b>Action</b><span>discrete or continuous action tokens</span></div>
</div>

Key idea: the model can use language reasoning and visual features before choosing robot actions.

::right::

<figure class="project-figure">
  <img src="https://openvla.github.io/static/images/openvla_model.jpg" alt="OpenVLA architecture showing image and language inputs mapped to robot actions" />
  <figcaption>OpenVLA project figure: image and instruction tokens are decoded into robot actions.</figcaption>
</figure>



---
layout: two-cols
---

# VLA Strengths and Failure Modes

**Strengths**

- Can follow new language instructions.
- Can reuse internet-scale visual knowledge.
- Can generalize across objects and tasks better than narrow policies.

**Failure modes**

- Spatial precision can be hard.
- Rare robot states may be underrepresented.
- Language can sound confident even when control is uncertain.

::right::

<div class="project-grid">
  <div>
    <video autoplay muted loop playsinline controls>
      <source src="https://openvla.github.io/static/videos/qualitative_results/correct_target/openvla--put_eggplant_into_pot--clutter.mp4" type="video/mp4" />
    </video>
    <span>Put Eggplant into Pot</span>
  </div>
  <div>
    <video autoplay muted loop playsinline controls>
      <source src="https://openvla.github.io/static/videos/qualitative_results/correct_target/openvla--put_corn_on_plate--clutter.mp4" type="video/mp4" />
    </video>
    <span>Put Yellow Corn on Pink Plate</span>
  </div>
  <div>
    <video autoplay muted loop playsinline controls>
      <source src="https://openvla.github.io/static/videos/qualitative_results/good_lang_cond/openvla--lift_red_chili_pepper.mp4" type="video/mp4" />
    </video>
    <span>Lift Red Chili Pepper</span>
  </div>

  <div>
    <video autoplay muted loop playsinline controls>
      <source src="https://openvla.github.io/static/videos/qualitative_results/good_lang_cond/openvla--lift_cheese.mp4" type="video/mp4" />
    </video>
    <span>Lift Cheese</span>
  </div>
  <div>
    <video autoplay muted loop playsinline controls>
      <source src="https://openvla.github.io/static/videos/qualitative_results/good_lang_cond/openvla--put_pink_cup_on_plate.mp4" type="video/mp4" />
    </video>
    <span>Put Pink Cup on Plate</span>
  </div>
  <div>
    <video autoplay muted loop playsinline controls>
      <source src="https://openvla.github.io/static/videos/qualitative_results/good_lang_cond/openvla--put_blue_cup_on_plate.mp4" type="video/mp4" />
    </video>
    <span>Put Blue Cup on Plate</span>
  </div>
</div>

---
layout: two-cols
---

# Example: VLA Models


- OpenVLA is an open-source 7B vision-language-action model trained on 970k robot episodes from Open X-Embodiment. It takes an image plus a language instruction and predicts robot actions. [Project](https://openvla.github.io/) | [Paper](https://arxiv.org/abs/2406.09246)
- In the OpenVLA example, the model maps commands like object placement or lifting tasks directly into robot control from visual input. [Teaser video](https://openvla.github.io/static/videos/openvla_teaser_video.mp4)
- It is a useful VLA example because the code, model weights, and training pipeline are all public. [GitHub](https://github.com/openvla/openvla) | [Hugging Face model](https://huggingface.co/openvla/openvla-7b)

::right::

<figure class="online-figure vla-teaser-figure mb-4">
  <img src="https://openvla.github.io/static/images/openvla_teaser.jpg" alt="OpenVLA model architecture" />
</figure>

<div class="video-card vla-teaser-video">
  <video autoplay muted loop playsinline controls>
    <source src="https://openvla.github.io/static/videos/openvla_teaser_video.mp4" type="video/mp4" />
  </video>
</div>

<div class="caption">OpenVLA project video: image + instruction → action.</div>

---
layout: two-cols
class: big-heading
---

# Generalist Policies 

Generalist robot policies aim to train once on many tasks, robots, and datasets, then adapt to a new setup.

- Instead of learning one narrow skill, they learn broad robot experience.
- Octo is a strong example of this style.
- The hope is similar to foundation models: pretrain broadly, then specialize quickly.

::right::

<figure class="project-figure">
  <img src="https://octo-models.github.io/teaser.jpg" alt="Octo project teaser" />
  <figcaption>Octo is designed as a generalist policy trained across many robot datasets.</figcaption>
</figure>

---
layout: two-cols
---

# Before Robotics: Foundation Models

The generalist-policy idea mirrors what happened in language and vision foundation models.

- Pretrain on a huge, diverse dataset
- Learn broad reusable representations
- Fine-tune or adapt for a specific downstream task

In robotics, the challenge is harder because datasets come from different robots, sensors, and action spaces.

::right::


<div class="origin-grid">
  <div>
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQKcoksYoCdX7airb81ZBmNUiht-0oaRSq2ww&s" alt="Diffusion image generation process from noise to image" />
    <span>Models trained on various modalities and able to output at various modalities</span>
  </div>
  <div>
    <div class="video-card">
      <video autoplay muted loop playsinline controls>
        <source src="https://generalistai.com/assets/videos/homepage/gen1-teaser.mp4" type="video/mp4" />
      </video>
    </div>
    <span>One robot models can learn from any type of data to perform generalist tasks</span>
  </div>
</div>

---
layout: two-cols
---

# Learning from Everything


- Mixes demonstrations from many robots, cameras, tasks, and environments.
- Standardizes each episode into observations, goals, robot state, and actions.
- Learns reusable manipulation patterns from broad robot experience.
- Uses language or goal images to condition the policy.
- Predicts short action sequences, then replans as the scene changes.
- Adapts to new tasks with much less data than training from scratch.


<!-- - Pretrained on many robot episodes from Open X-Embodiment.
- Supports flexible cameras, robot states, and action spaces.
- Start from a capable policy, then adapt.
 -->

::right::

<div class="origin-grid origin-grid-tall">
<figure class="online-figure octo-architecture-figure mb-4">
  <img src="https://octo-models.github.io/architecture.jpg" alt="Octo architecture diagram" />
</figure>

<figure class="online-figure octo-architecture-figure mb-4">
  <img src="https://octo-models.github.io/sampling_weights.jpg" alt="Octo sampling weights figure" />
</figure>
</div>



---
layout: default
---

# Comparing the Models

<table class="model-table">
  <thead>
    <tr>
      <th>Model family</th>
      <th>Input</th>
      <th>Training data</th>
      <th>Action style</th>
      <th>Advantages</th>
      <th>Limitations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Diffusion Policy</td>
      <td>Images + state history</td>
      <td>Task demonstrations from one robot setup</td>
      <td>Denoised action sequence</td>
      <td>Smooth continuous control; handles multiple valid futures</td>
      <td>Can be slower at inference; needs strong demonstration data</td>
    </tr>
    <tr>
      <td>ACT</td>
      <td>Multi-camera images + joints</td>
      <td>Teleoperated demonstrations</td>
      <td>Action chunks</td>
      <td>Data-efficient imitation; good for precise bimanual tasks</td>
      <td>Often specialized to one setup; less language reasoning</td>
    </tr>
    <tr>
      <td>VLA</td>
      <td>Image + language + state</td>
      <td>Vision-language data plus robot episodes</td>
      <td>Action tokens</td>
      <td>Strong language grounding; can reuse vision-language pretraining</td>
      <td>Large models are expensive; robot action grounding is hard</td>
    </tr>
    <tr>
      <td>Foundation Models</td>
      <td>Language or goal image + observations</td>
      <td>Mixed datasets across robots and tasks</td>
      <td>Diffusion-decoded actions</td>
      <td>Pretrain once, adapt broadly across tasks and robots</td>
      <td>Needs diverse datasets; embodiment differences are difficult</td>
    </tr>
  </tbody>
</table>

---
layout: default
---

# Why End-to-End Robotics is Exciting

- Turns robot behavior into a learning problem instead of a hand-designed pipeline.
- Lets demonstrations become direct supervision for perception and control.
- Makes language and vision natural inputs for specifying tasks.
- Allows one model family to cover many skills, robots, and environments.
- Gets better as datasets, compute, and foundation models improve.


<div class="benefit-wheel">
  <div>Less manual engineering</div>
  <div>Learns from data</div>
  <div>Uses foundation models</div>
  <div>Handles visual complexity</div>
  <div>Generalizes across tasks</div>
</div>

---
layout: default
---

# Why It Is Hard

<div class="grid-2 mt-8">
  <div class="card"><b>Data</b><br/>Robots need many high-quality examples.</div>
  <div class="card"><b>Safety</b><br/>Wrong actions can damage objects or hurt people.</div>
  <div class="card"><b>Generalization</b><br/>New lighting, objects, or rooms can break policies.</div>
  <div class="card"><b>Evaluation</b><br/>Success is physical, not just digital.</div>
</div>

<div class="risk-meter mt-7">
  <span>data scarcity</span>
  <span>safety risk</span>
  <span>distribution shift</span>
  <span>physical testing</span>
</div>

---
layout: two-cols
---

# Solution: Scale Better Data

Robots need more diverse experience before they can generalize.

- Pool demonstrations across robots, labs, tasks, and environments.
- Convert each dataset into a shared format for observations, goals, states, and actions.
- Pretrain policies on broad robot experience before adapting to a specific setup.

Example: [OpenX Embodiment, DROID](https://github.com/google-deepmind/open_x_embodiment)

::right::

<div class="origin-grid origin-grid-tall">
<figure class="online-figure octo-architecture-figure mb-4">
    <img src="https://github.com/google-deepmind/open_x_embodiment/raw/main/imgs/teaser.png" alt="Chatbots: Vision-language models" />
      <figcaption>1 Million Episodes</figcaption>
</figure>

<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://droid-dataset.github.io/videos/dataset-visualizer.mp4" type="video/mp4" />
  </video>
</div>

</div>




---
layout: two-cols
---

# Solution: Collect Cheaper Demos

High-quality robot data is expensive, so the collection process matters.

- Use low-cost teleoperation systems to make demonstrations easier to gather.
- Let humans provide corrective examples for hard edge cases.
- Focus data collection on tasks where real contact and dexterity matter.

Example: [Mobile ALOHA](https://mobile-aloha.github.io/)

::right::


<div class="origin-grid origin-grid-tall">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://umi-gripper.github.io//videos/in_the_wild_cup_data_overview.mp4" type="video/mp4" />
  </video>
</div>  

<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://umi-gripper.github.io//videos/in_the_wild_cup_data_collection.mp4" type="video/mp4" />
  </video>
</div>
</div>

<!-- <div class="origin-grid origin-grid-tall">
<figure class="online-figure octo-architecture-figure mb-4">
    <img src="/images/memo.png" alt="Chatbots: Vision-language models" />
</figure>

<!-- <div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://v.redd.it/0nw0ml4yvd2g1/HLSPlaylist.m3u8?f=hd%2CsubsAll%2ChlsSpecOrder&v=1&a=1780468313%2CODBlMzY0ODU2NGI2YzI5NWM2MTk0NWM0ZTQ3M2Y2MjU2MzI0ZDE0MzdjZDg3NzBjZTQ3YzA1MWNmZWVlZDMwNg%3D%3D" type="video/mp4" />
  </video>
</div>  -->

<!-- </div> -->
---
layout: two-cols
---

# Solution: Train With Variation

Policies fail when deployment looks different from training.

- Train in many simulated versions of the task, not one fixed scene.
- Randomize appearance and layout so the policy learns the task, not the background.
- Combine real demonstrations with synthetic trajectories.
- Use parallel simulation to test many conditions before hardware deployment.
- Reduce the sim-to-real gap by exposing the model to messy variation early.


Example: [NVIDIA Isaac Sim](https://investor.nvidia.com/news/press-release-details/2025/NVIDIA-Announces-Isaac-GR00T-N1--the-Worlds-First-Open-Humanoid-Robot-Foundation-Model--and-Simulation-Frameworks-to-Speed-Robot-Development/default.aspx)

::right::


<div class="origin-grid origin-grid-tall">
  <div>
    <img src="https://developer-blogs.nvidia.com/wp-content/uploads/2025/01/isaac-teleoperation.gif" alt="Diffusion image generation process from noise to image" />
  </div>
  <div>
    <div class="video-card">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/8Mwrfvq-GeY?si=UvAn1KmT6SkrO9BV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
    </div>
  </div>
</div>






---
layout: two-cols
---

# Solution: Deploy Cautiously

Learning-based policies still need guardrails in the real world.


- Deploy to learn what works on real hardware, not only in datasets.
- Use real failures to improve data collection and model training.
- Target useful tasks where hand-written pipelines struggle with variation.
- Start with constrained settings because physical mistakes are costly.
- Expand autonomy only after testing safety, reliability, and recovery.



Example: [Ultra robotics](https://www.ultra.tech/)

::right::


<div class="origin-grid origin-grid-tall">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://packaged-media.redd.it/706tmy4j0yxg1/pb/m2-res_468p.mp4?m=DASHPlaylist.mpd&var=sgpssan&v=1&e=1777896000&s=c30dc8010cded3274c4a4ab237fc6850ee2ed122" type="video/mp4" />
  </video>
</div>  

<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="/videos/end2end.mp4" type="video/mp4" />
  </video>
</div>
</div>


---
layout: two-cols
---

# How Do We Evaluate a Robot?

- Task Success: Did the robot complete the goal in the real world?
- Robustness: Does it still work when lighting, object positions, camera views, or backgrounds change?
- Recovery: Can it correct mistakes, retry a grasp, or continue after a small failure?
- Safety: Does it avoid collisions, excessive force, unstable motions, or risky behavior near people?
- Efficiency: How long does the task take, and how many actions or retries are needed?
- Generalization: Does the policy work on new objects, new rooms, or new task instructions?
- Reliability: What is the success rate over many repeated trials, not just one demo?

::right::

<div class="origin-grid ">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://packaged-media.redd.it/zrysycrr7uvg1/pb/m2-res_720p.mp4?m=DASHPlaylist.mpd&var=sgpssan&v=1&e=1777896000&s=4220f0cbddf83831c594998752ffa561780b19a2" type="video/mp4" />
  </video>
</div>  

</div>


<!-- ::right::

<div class="eval-board">
  <div><b>92%</b><span>success</span></div>
  <div><b>0</b><span>collisions</span></div>
  <div><b>5</b><span>new objects</span></div>
  <div><b>10</b><span>demos</span></div>
</div> -->


---
layout: center
class: text-center
---

# Key Takeaway

<div class="big-quote">
End-to-end robotics learns a direct path from perception to action compared to tradition human engineered solutions, but scaling data, real-world safety and generalization remain major challenges.
</div>


---
layout: center
class: text-center
---

# Companies at the Forefront

<div class="big-quote">
There are many companies trying to push for commercial deployment of these solutions already. This was unheard of only a few years ago.
</div>

---
layout: center
class: text-center
---



# Ultra Robotics

<div class="origin-grid ">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://ultratech.b-cdn.net/OPTIMIZED%20FOR%20PERFORMANCE%20AND%20SAFETY%20V2.mp4" type="video/mp4" />
  </video>
</div>  

</div>


---
layout: center
class: text-center
---

# Figure AI

<div class="origin-grid ">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="/videos/figure.mp4" type="video/mp4" />
  </video>
</div>  
</div>


---
layout: center
class: text-center
---

# Reflex Roboitcs/

<div class="origin-grid ">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://cdn.prod.website-files.com/6822b858ead5da1d444f23a3/6822b858ead5da1d444f23fd_0316%20(1)(11)-transcode.mp4" type="video/mp4" />
  </video>
</div>  
</div>



---
layout: center
class: text-center
---

# Sunday Robotics/

<div class="origin-grid ">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="/videos/sunday.mp4" type="video/mp4" />
  </video>
</div>  
</div>


---
layout: center
class: text-center
---

# Physical Intelligence /

<div class="origin-grid ">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://website.pi-asset.com/pi06star/cafe_100x.mp4" type="video/mp4" />
  </video>
</div>  
</div>


---
layout: center
class: text-center
---

# Generalist /

<div class="origin-grid ">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
    <source src="https://generalistai.com/blog/apr-02-2026-GEN-1/assets/generalist-gen1-box-folding-200.mp4" type="video/mp4" />
  </video>
</div>  
</div>


---
layout: center
class: text-center
---

# Sklid AI /

<div class="origin-grid ">
<div class="video-card">
  <video autoplay muted loop playsinline controls>
   <source src="https://dtkk46np7h1p6.cloudfront.net/videos/Long-Form-Clip2.mp4" type="video/mp4" />
  </video>
</div>  
</div>





---
layout: center
class: text-center
---

# Discussion

Would you trust an end-to-end robot in a home, hospital, or factory?

<div class="mt-14 opacity-70">What would it need to prove first?</div>

---
layout: default
---

# Reinforcement Learning, A While New Shift In Robot Control


<div class="video-card">
<iframe width="560" height="315" src="https://www.youtube.com/embed/srPz8TRpZ_8?si=uXoyDOH3ufTbcJvY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
