# Summary
This is the web application version of the WorkflowCombo command line tool.

# To-Do's
1. Eventually I'd like to allow the user to drag and drop the files they input to determine the order in which they will be organized in the workflow (rather than renaming the files to start with 01, 02, etc..)
2. I'd like to split this webpage down the middle and have the questions on the left side, and a preview of the workflow they're building on the right side (so they know what it looks like)
3. I'd like to tighten the regex for parsing the inputs and outputs of the CWL data. Right now, they're very specific to the somatic example files that Dr. Piccolo provided, but I'd like to write some better regex that matches what ToolJig creates.

# History
Please delete this section later, I just wanted a place to document the transition from using regex to using a package called "js-yaml" that will read and parse the incoming CWL files. 
This is the regex code I wrote before I switched. 
            selectedFile: function() {
                console.log('selected a file or multiple files');
                console.log(this.$refs.myFile.files[0]);
                let i;
                for(i=0; i < this.$refs.myFile.files.length; i++){
                    let file = this.$refs.myFile.files[i];
                    this.list_of_names.push(file.name)
                    this.text1 = this.text1 + file.name // this line is for debugging

                    if(!file) return;
                    let reader = new FileReader();
                    reader.readAsText(file, "UTF-8");
                    reader.onload =  evt => {
                        let doc = jsyaml.safeLoadAll(evt.target.result);
                        this.text = this.text + doc.toString()
                    }
                    reader.onerror = evt => {
                        console.error(evt);
                    }
                }
                this.text1 = this.uploaded_CWL_FileNames.toString()
            },
            separateInputs: function(newInput){
                let inputName = "";
                let inputType = "";
                let inputDoc = "";
                let toolInputMap = new Map()

                while (newInput.length !== 0) {
                    // find name and get rid of it
                    inputName = newInput.match(/\w*(?=:)/)[0].toString()
                    newInput = newInput.replace(/\w*(:)/, "")
                    // find type and get rid of it
                    inputType = newInput.match(/(?<=type:\s)\w*/)[0].toString()
                    newInput = newInput.replace(/(type:\s)\w*/, "")
                    // find doc and get rid of it
                    inputDoc = newInput.match(/(?<=doc:)[\s\S]*?((?=\w*:)|$)/)[0].toString()
                    newInput = newInput.replace(/(doc:)[\s\S]*?((?=\w*:)|$)/, "")
                    let dictMap = new Map([
                        ['name', inputName],['type', inputType],['doc', inputDoc]
                    ])
                    toolInputMap.set(inputName, dictMap)

                    try {
                        newInput.match(/\w*(?=:)/)[0].toString()
                    } catch (error) {
                        break;
                    }

                }
                return toolInputMap;
            },

