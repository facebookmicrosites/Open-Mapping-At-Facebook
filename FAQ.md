# General Questions about Map With AI

**What is Map with AI?**

“Map With AI” is a service designed for helping the OpenStreetMap (OSM) community. By facilitating mappers with AI-generated features through the RapiD Editor, it helps achieve faster mapping speed and higher data quality. It is publicly available at https://mapwith.ai.

**Who can use it?**

The https://mapwith.ai website is open to everyone. However, users do need to have an official OSM account to use our tools and follow the [OSM mapping guidelines](https://wiki.openstreetmap.org/wiki/Good_practice) when contributing to OSM.

**Where can the OSM community go to access the tool?**

You can access the RapiD editor though the “Start Mapping” links at https://mapwith.ai/.

**What is RapiD Editor?**

Thousands of mappers use a tool called the iD editor to add features to OpenStreetMap worldwide. Facebook's World.AI team has taken this popular map editing tool and enhanced it. The new tool, RapiD Editor, helps mappers map more efficiently by providing roads auto-detected from satellite imagery and includes additional data integrity checks to ensure the quality of new map edits.

**Why does facebook develop the RapiD editor while there is already the iD editor avaiable to the community?**

The RapiD editor is simply an enhancement of the current iD tool, so the user experience will be the same with added road-mapping features and integrity checks. 

**How does Map with AI work?**

Using artificial intelligence it predicts features on high-resolution satellite imagery, then they get populated in our RapiD map editing tool.

**In which countries is Map With AI available?**

We currently have data available in Afghanistan, Bangladesh, Indonesia, Mexico, Nigeria, Tanzania, and Uganda and we are working on adding more data in other countries.

**Has anyone outside of Facebook tried or tested Map With AI?**

Yes, we have been testing with partners for months to gather feedback and fix bugs. 

**Are there any limitations with AI?**

While AI is efficient and continues to improve, human mappers are essential to review and manually input anything missed. However, we are excited by the possibilities of AI for tackling challenges in the future such as assigning tags according to OSM region-specific guidelines or building OSM relations for complex features.

**Is human validating required for adding roads to OSM?**

Yes, every single road from the AI output will be added only after human validation. Mappers must manually select a road to OSM from the RapiD layer so every road will receive human attention. Our additional validation checks then help to ensure that common data errors from our RapiD roads are flagged for the editor to fix. 

**How can Map with AI improve road mapping for certain communities?**

We can take advantage of this technology to aid communities around the world in disaster response areas and where people are still unconnected.

For example, in August of 2018, Kerala, India experienced a severe flooding event that covered much of the state and affected millions. To aid in the response, the local OSM community reached out to Facebook for assistance mapping out missing roads in the affected areas using our machine learned data. Within a few days of getting the data prepared, the team of 34 mappers from Facebook was able to import over 21500 roads into the map.

# Questions about AI-generated Roads and RapiD Usage

**How can I track RapiD changesets?**

All RapiD changesets will include the tag “created_by - RapiD 0.9.0” (or current version number) and assuming the default imagery isn’t changed “imagery_used - Facebook's Map With AI - Maxar Imagery”.

**Why not put the “source” tag on the changeset instead of every single feature?**

We have been asked by community members before to identify data coming from Facebook services in a more specific way, so we decided to tag individual features along with changeset comments.

**Is all RapiD data open source?**

All data provided through RapiD is open source under the [MIT license](https://opensource.org/licenses/MIT).

**Why are certain segments picked up and others are not?**

There are many reasons that RapiD can fail to pick up a road. Sometimes the area is obscured or may just look different from what the AI has seen before so it isn’t picked up by the machine. Other times, the post processing of the raw predictions into RapiD data can fail or have bugs. We are actively working on both issues but it is a difficult problem to solve completely. 

**How will you ensure that people do not just bulk upload data?**

The quality of the mapping contributions is a major priority; this is why we have the validation panel to inform the user about potential issues, and the list of the checks could be expanded in the future. We are also making sure that accidental “bulk” uploads are impossible – the user has to manually select the roads one-by-one from the magenta layer and click “use this feature” in order to start working with it. Additionally, when users access RapiD directly without going through a managed project in HOT Tasking Manager, we only allow 50 AI-generated roads to be added in each mapping session to keep changesets a reasonable size.

**Will you offer JOSM support?**

We are considering supporting JOSM in the future, but for now are focusing on improving RapiD.

**Have you addressed imagery offsets?**

Imagery offsets are a hard problem to address. Our current approach is to minimize any change to the existing OSM data, so our algorithms behave very similarly to what the human user would do – generate the roads for a particular satellite image layer, and merge it with the existing data. We encourage RapiD users to use the existing OSM data and available GPX data to ensure proper alignment when mapping.

**How are you deciding the types (highway tags) for RapiD added roads?**

We are using similar AI methods used for detecting roads in order to predict highway tags. However tagging is a much harder problem to solve than road identification so editors may need to change the suggested tag upon adding the RapiD road. We are actively working on making the predictions better, but the fundamental complexity of the problem is compounded by road tagging being different depending on the locality.

**How does connection creation logic work in RapiD? why are some connections not created automatically?**

RapiD has some automatic connection logic built in, but tries to be conservative when a pre-existing or AI-generated road has been moved manually compared to the original predicted connection location. The crossing-way validation check will be able to catch the missed connections and suggest possible fixes to the user.

**Why does RapiD crop roads at task boundaries? Are you concerned about the risk of creating disconnected ways?**

We believe this is a general problem when working on tiled mapping tasks. We learnt from the community that when working on tasks on HOT Tasking Manager, a general guideline for the mappers is to draw roads up to the task boundary to avoid creating dupes across tasks, so RapiD is designed to align with this guideline. When the user is working on the neighbor task later, the close-node check or crossing-way check will have a chance to catch the disconnected ways and help the user fix them.

**Compared to iD, what are the extra validation checks that you have built into RapiD?**

Some validation checks that we started from RapiD have already been contributed and merged into iD, e.g. detection for **island of disconnected roads** and **close nodes on roads**. Besides those, RapiD also does two extra checks:

**Excessive nodes around connections:** some AI-generated roads could be too detailed around connections and make a connection look like “Y” shaped. This check helps catch those cases and suggests fixes by deleting the excessive nodes around connections.

**Short roads:** some AI-generated roads are shorter than 20 meters. In reality, some of them don’t serve a practical purpose for people, and some of them need to be extended to reach a house or another road. So we added this check to flag these candidates for extra manual edits.

To understand how these validation checks work in practice, please refer to our [training document](https://github.com/facebookmicrosites/Open-Mapping-At-Facebook/wiki#validation-checks).
