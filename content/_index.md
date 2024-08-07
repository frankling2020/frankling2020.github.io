---
# Leave the homepage title empty to use the site title
title:
date: 2022-10-24
type: landing

sections:
  - block: about.biography
    id: about
    content:
      title: Biography
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
  - block: collection
    id: featured
    content:
      title: Featured Work
      filters:
        folders:
          - publication
        featured_only: true
    design:
      columns: '2'
      view: card
  - block: portfolio
    id: projects
    content:
      title: Projects
      filters:
        folders:
          - project
      # Default filter index (e.g. 0 corresponds to the first `filter_button` instance below).
      default_button_index: 0
      # Filter toolbar (optional).
      # Add or remove as many filters (`filter_button` instances) as you like.
      # To show all items, set `tag` to "*".
      # To filter by a specific tag, set `tag` to an existing tag name.
      # To remove the toolbar, delete the entire `filter_button` block.
      buttons:
        - name: All
          tag: '*'
        - name: Deep Learning
          tag: Deep Learning
        - name: Data Science
          tag: Data Science
        - name: Big Data
          tag: Big Data
        - name: Statistics
          tag: Statistics
        - name: Other
          tag: Demo
    design:
      # Choose how many columns the section has. Valid values: '1' or '2'.
      columns: '1'
      view: showcase
      # For Showcase view, flip alternate rows?
      flip_alt_rows: false
  - block: collection
    id: posts
    content:
      title: Posts
      subtitle: ''
      text: ''
      # Choose how many pages you would like to display (0 = all pages)
      count: 0
      # Filter on criteria
      filters:
        folders:
          - post
        author: ""
        category: ""
        tag: ""
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ""
      # Choose how many pages you would like to offset by
      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      # Choose a layout view
      view: compact
      columns: '2'
  - block: experience
    id: experience
    content:
      title: Experience
      # Date format for experience
      #   Refer to https://wowchemy.com/docs/customization/#date-format
      date_format: Jan 2006
      # Experiences.
      #   Add/remove as many `experience` items below as you like.
      #   Required fields are `title`, `company`, and `date_start`.
      #   Leave `date_end` empty if it's your current employer.
      #   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
      items:
        - title: Graduate Student Instructor
          company: School of Information, University of Michigan
          company_url: 'https://www.si.umich.edu/'
          company_logo: umlogo
          location: Michigan
          date_start: '2023-08-28'
          date_end: ''
          description: |2-
              Responsibilities include:
              * SI 671 Data Mining Discussion
        - title: Research Intern
          company: Michigan Traffic Lab
          company_url: 'https://traffic.engin.umich.edu/'
          company_logo: umlogo
          location: Michigan
          date_start: '2023-04-01'
          date_end: '2023-08-27'
          description: |2-
              Responsibilities include:
              * Deploying the McityGPT with LangChain to introduce Mcity to newcomers with useful information from the website.
              * Understanding the basics of importance sampling and natural driving enviornment.
              * Researching on the autonomous vehicle safety test with Traci sumo by modelling the traffic accidents in the natural adversarial driving environment (NADE).
              * Calibrating the distribution of traffic accidents with experiments in Great Lakes.
        - title: Research Assistant
          company: Shanghai Jiao Tong University
          company_url: ''
          company_logo: sjtulogored
          location: Shanghai
          date_start: '2022-03-01'
          date_end: '2022-08-04'
          description: |2-
              Responsibilities include:
              * Understood the basics of GNN including GCN and GAT and the usage of PyTorch and PyTorch Geometric.
              * Compared GNN with Computer Vision and Natural Language Processing in data augmentation and searched for similarities.
              * Investigated contrastive learning methods in graph representation learning and fine-tuned models with random masking and attention masking.
        - title: Teaching Assistant
          company: UM-SJTU Joint Institute
          company_url: 'https://umji.sjtu.edu.cn/'
          company_logo: sjtulogored
          location: Shanghai
          date_start: '2021-05-01'
          date_end: '2021-12-08'
          description: |2-
              Responsibilities include:
              * Taught Physics and Circuit theory by providing RC and OH for around 150 students.
              * Scored homeworks and exams and prepared exam questions.
              * Obtained praise as a teaching assistant. 
    design:
      columns: '2'
  - block: collection
    content:
      title: Recent Work
      text: |-
        {{% callout note %}}
        Quickly discover relevant content by [filtering publications](./publication/).
        {{% /callout %}}
      filters:
        folders:
          - publication
        # exclude_featured: true
    design:
      columns: '2'
      view: citation
  - block: accomplishments
    content:
      # Note: `&shy;` is used to add a 'soft' hyphen in a long heading.
      title: 'Accomplish&shy;ments'
      subtitle:
      # Date format: https://wowchemy.com/docs/customization/#date-format
      date_format: Jan 2006
      # Accomplishments.
      #   Add/remove as many `item` blocks below as you like.
      #   `title`, `organization`, and `date_start` are the required parameters.
      #   Leave other parameters empty if not required.
      #   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
      items:
        - certificate_url: https://www.coursera.org/account/accomplishments/certificate/3RMKGFQJWU4W
          date_end: '2022-01-08'
          date_start: '2022-01-01'
          description: ''
          organization: Coursera
          organization_url: https://www.coursera.org
          title: Advanced Computer Vision with TensorFlow
          url: 'https://www.coursera.org/learn/advanced-computer-vision-with-tensorflow'
        - certificate_url: https://www.coursera.org/account/accomplishments/certificate/57RSFK4Y3HSM
          date_end: '2021-08-18'
          date_start: '2021-08-11'
          description: ''
          organization: Coursera
          organization_url: https://www.coursera.org
          title: Neural Networks and Deep Learning
          url: 'https://www.coursera.org/learn/neural-networks-deep-learning'
    design:
      columns: '2'
  - block: contact
    id: contact
    content:
      title: Contact
      subtitle:
      text: |-
        My research interests include artificial intelligence, information retrieval, and programmable matter. If you are interested in working together or have any questions, please feel free to contact me using the information below. I would love to hear about any opportunities that may be a good fit for my skills and experience.
        
        <div class="mb-3"></div>
        <script async defer type="text/javascript" id="clustrmaps" src="//clustrmaps.com/map_v2.js?d=eEBExyqiZgc8xPI7VBGj7e6Z_PW4ygN37kaU59B-O64&cl=ffffff&w=a"></script>
      # Contact (add or remove contact options as necessary)
      email: 'carofrank2000@gmail.com'
      # Automatically link email and phone or display as text?
      autolink: true
      # Email form provider
      # form:
      #   provider: formspree
      #   formspree:
      #     id:
      #   # netlify:
          # Enable CAPTCHA challenge to reduce spam?
          # captcha: false
    design:
      columns: '2'
---
