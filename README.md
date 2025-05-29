<html>
    <head>
        <style>
            card{
                width: 40%;
            }
        </style>
    </head>
    <body>
        <div className="card bg-white dark:bg-white/[0.03]">
            <div className="flex flex-col gap-6 lg:flex-row lg:items-start lg:justify-between">
              <div>
                <h4 className="card-title">Profile Details</h4>
                <div className="grid grid-cols-1 gap-4 lg:grid-cols-2 lg:gap-7 2xl:gap-x-32">
                  <div>
                    <p className="subheader">First Name</p>
                    <p className="content">Harmeet</p>
                  </div>
                  <div>
                    <p className="subheader">Last Name</p>
                    <p className="content">Arora</p>
                  </div>
                  <div>
                    <p className="subheader">Email</p>
                    <p className="content">harmeeta2@gmail.com</p>
                  </div>
                  <div>
                    <p className="subheader">phone</p>
                    <p className="content">7972195259
                    </p>
                  </div>
                  <div>
                    <p className="subheader">Date of Birth</p>
                    <p className="content">2025-08-02
                    </p>
                  </div>
                  <div>
                    <p className="subheader">Total Experience in months</p>
                    <p className="content">111
                    </p>
                  </div>
                  <div>
                    <p className="subheader">Notice Period</p>
                    <p className="content">null</p>
                  </div>
                  <div>
                    <p className="subheader">Expected Joining Date</p>
                    <p className="content">null</p>
                  </div>
                  <div>
                    <p className="subheader">cv_summary</p>
                    <p className="content">Currently working as a Content Writer with Astral Informatics Limited since Feb 2022.
                         Expertise in management and development of content for various websites. Passionate about learning new techniques and concepts.</p>
                  </div>
                  <div>
                    <p className="subheader">Current salary</p>
                    <p className="content">Current salary</p>
                  </div>
                  <div>
                    <p className="subheader">Expected salary</p>
                    <p className="content">Expected salary</p>
                  </div>
                  <div>
                    <p className="subheader">Gender</p>
                    <p className="content">Female</p>
                  </div>
                  <div>
                    <p className="subheader">city</p>
                    <p className="content">city</p>
                  </div>
                </div>
              </div>
              <button onClick={openModal} className="edit-button">
                <PencilIcon className="w-5 h-5" />
                Edit
              </button>
            </div>
          </div>
    </body>
</html>
