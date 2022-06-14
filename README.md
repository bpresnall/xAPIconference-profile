# xAPIconference-profile
<h1>1.0 Overview</h1>
<p>This specification describes interoperable runtime communication between Conference website and LRS.</p>
<h2>1.1 Scope</h2>
<p>The scope of this specification is limited to the following:</p>
<ul>
<li>Launch content by an conference website</li>
<li>Launch and runtime environment used by conference website</li>
<li>Reporting requirements for the conference website.</li>
</ul>
<p>This specification references how to use the xAPI specification within this scope.</p>
<h1><strong>2.0 Definitions</strong></h1>
<p>For purposes of this specification, the following terms and definitions apply:</p>
<ul>
<li><strong>Assignable Unit (AU)</strong>: A learning content presentation launched from an conference website. The AU is the unit of tracking and management. The AU collects data on the learner and sends it to the LMS.</li>
<li><strong>Experience API (xAPI)</strong>: A runtime data communication specification for learning content (AU) to send and receive data to a Learning Record Store (LRS). The xAPI specification referenced by this document is used to define the data transport and the data model.</li>
<li><strong>Internationalized Resource Identifier (IRI)</strong>: A unique identifier according to RFC 3987. The IRI may be an IRL. IRLs SHOULD be defined within a domain controlled by the person creating the IRL. Note that IRI&rsquo;s in this spec MUST be fully qualified and not IRI References.</li>
<li><strong>Learning Records Store (LRS)</strong>: As defined in the xAPI specification.</li>
<li><strong>Registration</strong>: An sign up instance of a learner in a conference website. (a registration ID uniquely identifies this).</li>
<li><strong>Session</strong>: A period of time marked by the user login until its termination (or abandonment).</li>
</ul>
<h1>3.0 Conformance</h1>
<p>Conformance to this specification is defined in this section.</p>
<p>In this specification:</p>
<ul>
<li>"MUST" is to be interpreted as a requirement on an implementation.</li>
<li>"MUST NOT" is to be interpreted as a prohibition.</li>
<li>"SHOULD" is to be interpreted as a recommendation for implementation.</li>
<li>"SHOULD NOT" is to be interpreted as the converse of "SHOULD".</li>
<li>"MAY" is to be interpreted as a course of action that is permissible within the limits of the specification.</li>
<li>"NEED NOT" is to be interpreted as a course of action that is not required.</li>
</ul>
<h2>3.1 Assignable Unit (AU)</h2>
<p>AU Requirements. An Assignable Unit MUST conform to all requirements as specified in the xAPI specification.</p>
<h2>3.2&nbsp; Conference Website</h2>
<p>Conference Website. The Conference Website MUST conform to all LRS requirements as specified in the xAPI specification.</p>
<p>The Conference Website MUST have an account which is able to retrieve all Resource data about another distinct user across multiple sessions for that user.</p>
<h1><strong>4.0 Conceptual Model: Informative</strong></h1>
<p>Synopsis of the Conference profile model:</p>
<ul>
<li>An Conference website include content, which may contain one or more AUs.</li>
<li>A learner authenticates with an conference website.</li>
<li>A learner launches an AU from the conference webisteusing an interface.</li>
<li>The conference website writes launch data to the integrated LRS.</li>
<li>The user views the AU content and performs the learning. During this time, the AU MAY request data from, and store data to, the website.</li>
<li>The learner exits the AU.</li>
</ul>
<p>Responsibilities of the Assignable Unit:</p>
<ul>
<li>Parse the parameters from the launching environment to determine where the website location is and initiate communication with the website.</li>
<li>Format all data according to the defined data types and vocabularies that are defined in this specification.</li>
<li>Send a "terminate" statement prior to terminating the AU's execution.</li>
</ul>
<p>Responsibilities of the website:</p>
<ul>
<li>Create and maintain content structures.</li>
<li>Format all data according to the defined data types and vocabularies that are defined in this specification.</li>
<li>Launch the specified AU contained in the courses within the defined environment(s).</li>
</ul>
<h1>xAPI Statement Data Model</h1>
<h2>1 Statement ID</h2>
<p>Each statement has unique statement id</p>
<h2>2 Actor</h2>
<p>The Actor property must be defined as per the xAPI Specification.</p>
<p>When user logged in to conference website it has unique user id, this id should be proceed as Actor in the statement</p>
<h2>3 Verbs</h2>
<p>One of these is required for every page.&nbsp;</p>
<p><strong>&ldquo;Required&rdquo; Verb</strong></p>
<p>Every time a page is &ldquo;launched&rdquo; from website verb launched must be sent to the xAPI Learning Record Store (LRS).</p>
<ul>
<li><strong>Initialized</strong><strong> - </strong>Indicates the actor logged in to the conference website.</li>
<li><strong>Launched</strong><strong> - </strong>Indicates that the actor open page.</li>
<li><strong>Attended &ndash; </strong>&nbsp;indicates the actor click on presentation link</li>
<li><strong>Commented &ndash; </strong>Indicate the actor commented any content - click on send comment button. Result reponse is comment text</li>
<li><strong>Rated &ndash; </strong>Used to rate presentation, result is in range (1,5).</li>
</ul>
<p>&nbsp;&nbsp;&nbsp;&nbsp; Video</p>
<ul>
<li><strong>Initialized<br /></strong>An "Initialized" statement is used to indicate that the video has been fully initialized or launched.&nbsp;</li>
</ul>
<ul>
<li><strong>Played<br /></strong>Used when the actor generally played a video or clicked the play button.&nbsp;</li>
</ul>
<ul>
<li><strong>Paused<br /></strong>Indicates that the actor temporary or permanently stopped experiencing the recorded media object.&nbsp;</li>
</ul>
<ul>
<li><strong>Seeked<br /></strong>Used in combination with time-from and time-to extensions when the Actor moves the progress bar forward or backward to a specific time in the video.<br />Id: <a href="https://w3id.org/xapi/video/verbs/seeked">https://w3id.org/xapi/video/verbs/seeked</a></li>
<li><strong>Interacted</strong></li>
</ul>
<p>Used to express that the actor interacted with the player (except play, pause, seek). e.g. mute, unmute, change resolution, change player size, etc.</p>
<p>Id: http://adlnet.gov/expapi/verbs/interacted</p>
<ul>
<li><strong>Completed<br /></strong>Used to express that the actor completed a video by watching all parts of the video at least once.<br />Id: http://adlnet.gov/expapi/verbs/completed</li>
</ul>
<ul>
<li><strong>Terminated<br /></strong>Used to express that the actor ended a video.</li>
</ul>
<p>Id: http://adlnet.gov/expapi/verbs/terminated</p>
<h2>4 Object</h2>
<p>An Object with objectType "Activity" MUST be present, as specified in the xAPI Spec.</p>
<p>The Object represents the page, presentation, video, comment consumed by the Actor.</p>
<h3>4.1 Definition</h3>
<p>Object definition MAY contain name, description and other details of the media, as per the xAPI Spec.</p>
<h2>5. Result</h2>
<p>Only commented and rated verbs have object result parts: for commented text of the comment is stored in the response and for the rated score is stored in the score raw.</p>
