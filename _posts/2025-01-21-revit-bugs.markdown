---
layout: post
title:  Revit Annoyances and Bugs
categories: revit programming
---

# Revit Annoyances and Bugs
A huge dump of the frustrations I have encountered with Revit

https://autodesk.my.site.com/customer/apex/Case_CustomerPortalLandingPage#

BUG: Family → Load into Project behaves unpredictably if two documents are open with the same name but different cases
Example: `Norgren R74G-4AK-RMG.rfa` and `Norgren r74g-4ak-rmg.rfa`

ForgeTypeId
GroupTypeId class instead of BuiltInParameterGroup?
GroupTypeId class functioning as an enum

Load Autodesk Family does not remember selection between browse filters
Sorting is case-sensitive

Project Browser Expand/Collapse syncs across users

Ctrl + Tab cycles forward, but Ctrl + Shift + Tab does not cycle backwards
    Manage Links

DMU documentation [[Notes - DMU and Triggers]]

[Missing Something in a Revit View? 33 Steps to Find Stuff | Ideate Inc](https://www.ideateinc.com/blog/2013/01/missing-something-in-revit-view-33)
[Can't see it in the view? Here's 33 reasons maybe why - Revit Forum](https://www.revitforum.org/forum/revit-all-flavors/tutorials-tips-tricks/459-can-t-see-it-in-the-view-here-s-33-reasons-maybe-why)
Ideate apps helps with [XRay]([Wishlist Granted! Why is a Revit Element Hidden in a View? (ideatesoftware.com)](https://ideatesoftware.com/wishlist-granted-why-is-a-revit-element-hidden)) for [$495/year](https://ideatesoftware.com/ideateapps-purchase)
[Why Revit is `****` (thinkmoult.com)](https://thinkmoult.com/why-revit-is-shit.html)

Opening plans often does not zoom to extents or otherwise set reasonable view bounds

Some endpoints use property get/set, but others use `Get___()` and `Set___()` functions
Example: `OverrideGraphicSettings.SetProjectionLineColor` but `OverrideGraphicSettings.ProjectionLineColor`

Purge Unused has to be run multiple times

`ConnectionValidationInfo.GetWarning` should be iterable

`TextNote` leaders in general
`IndependentTag` leaders are not the same as `TextNote` leaders
`TextNote` leader elbows have UI alignment hints, but `IndependentTag` leaders do not

`IndependentTag` `rev.GetLeaderElbow()` = `TextNote` `leader.elbow` = `SpotDimension` `LeaderShoulderPosition`

`ISelectionFilter` vs `ElementFilter`

View Sections have two different sets of grips that sometimes work together

`UIDoc.ActiveGraphicalView` is not the same as `active_view = next(iter(x for x in uidoc.GetOpenUIViews() if x.ViewId == uidoc.ActiveGraphicalView.Id), None)`

Need "Reveal selected family in Project Browser" context menu option

No ability to format tag dimension fractions as nice fractions ¼ ½ ¾

Trying to access some properties throws error
Example: `Group.Location.Rotation` does not work even with `getattr(element.Location, 'Rotation')`

Hard to tell whether things are parallel
Sometimes things are very close, but not actually up/down or left/right

FilteredElementCollector has not OfCategoryType filter

Some questions do not have a verb
Examples: `FamilyInstance.flipFacing()`, `FamilyInstance.flipHand()`
Counterexamples: `KeyBasedTreeEntriesLoadContent.CanAddEntry()`, `AdaptiveComponentFamilyUtils.IsAdaptivePoint(doc, refPointId)`

Generic Annotation has Label parameter in Properties panel, but Array does not

Insulation specification cannot be set with API if part has taps, but can be set in GUI

Properties panel does not allow Ctrl + Backspace/Arrows for text editing
Type Properties does not have accessibility shortcots for OK/Cancel/Apply

`Element.get_Parameter()`

`BuiltInParameter.RBS_CALCULATED_SIZE` no documentation on how this is calculated

Some objects implement both `return Element` and `return ElementId`, some `return Reference`
Example: `IndependentTag.GetTaggedLocalElements`, `IndependentTag.GetTaggedLocalElementIds`
Example: `ViewPlan.GenLevel` returns Level Element, no `GenLevelId` implemented; `ViewPlan.GetFilters()` returns `List[ElementId]`

Some methods take `Element`, some `ElementId`
Example: `Creation.Document.NewFamilyInstance(location, symbol, level, structuralType)`, `Selection.SetElementIds`
Example: `FilteredElementCollector(doc, levelId)`
`Category.AllowsVisibilityControl[View]`

Unusual behavior with `SpotDimension`, especially slope tags
`SpotDimensionType`

Family `Label` cannot be accessed:
- [Getting parameters assigned to a label](https://forums.autodesk.com/t5/revit-api-forum/getting-parameters-assigned-to-a-label/td-p/9487270)
- [List parameters used in a Label (TextElement) within a family document](https://forums.autodesk.com/t5/revit-ideas/list-parameters-used-in-a-label-textelement-within-a-family/idi-p/9491306)
- [[API] Get Shared Parameter linked to a Label](https://forums.autodesk.com/t5/revit-ideas/api-get-shared-parameter-linked-to-a-label/idi-p/7077420)
# File Handling
Revit flashes every time Explorer is opened

Project Browser → Right-click Search → enter shows next match, but shift + enter does not show previous

Most file dialogs (like Load Family) do not allow pasting a path surrounded by quotes (from Shift + Click on a file in Explorer → Copy as path)
Most dialog boxes show up on primary monitor instead of monitor where Revit is displayed




# Tags
IndependentTag has no BoundingBox without leaders
IndependentTag will not rotate to vertical with leader elbow if only one leader/host
IndependentTag with orientation Horizontal still vertical when tagging vertical pipes, except when leader has an elbow

`IndependentTag.AddReferences` refers to `TagMode`, which is not a valid property (only present in `IndependentTag.Create()`)
Defined by `IsMaterialTag` and `IsMulticategoryTag`?

No easy way to find out which elements can be properly tagged with a given tag

No align options for label

Rotating tagged duct accessory family deletes the tag

`IndependentTag.Create()` docs say `referenceToTag` "can be to an element or subelement in a local or linked document" but reference from `Selection.PickObject(ObjectType.PointOnElement)` fails with `The reference can not be tagged.`
# Fabrication
Fabrication Parts do not obey button codes or button mapping from CADmep

Some created parts have their Origin set to something other than `(0, 0, <level elevation>)`

Fabricatiion Parts → Edit Part does not show connectors intuitively [Autodesk Fabrication - Determining C1/C2 Connectors in Revit - BIM there. Done that. (darrenjyoung.com)](https://www.darrenjyoung.com/2021/11/04/autodesk-fabrication-determining-c1-c2-connectors-in-revit/)

`Connector` (for parts?) vs `ConnectorElement` (for families?)
Direction property conflict
`ConnectorManager.Connectors` order is randomly changed


# Families
Array of extrusions silently breaks constraints
Locking alignment of array of extrusions silently breaks constraints?
Selecting array item does not show constraints or lock icon

Array count is called "Label" and hard to find -- click on array element, click on array spanning line, use Modify | Array bar

Family / Symbol / FamilyInstance inconsistent naming between family editor and document


Edit family inside edit family → Load into Project should have quick option to load into document from which editing was launched
Load into Project file picker is confusing if multiple files have similar names

Double-click does not accept selected option in many places
 - Associate Family Parameter

`FamilyManager.GetParameter()` and `GetAssociatedFamilyParameter()` does not accept `Element.Parameter.GetAssociatedGlobalParameter()` output
Use `FamilyManager.GetAssociatedFamilyParameter(Element.Parameter)` instead

Connector `MEPSystemClassification` makes no distinction between pipe, duct, and electrical connectors

Model lines cannot be locked to reference planes
Dimension to a model line that has been locked to a reference plane, then assign a family parameter to the dimension. The model line becomes unlocked.
## Family Type Editor
No easy way to discern between family parameters and shared parameters

Ctrl + Shift + Arrow Left/Right has weird behavior, should select adjacent word
Change a parameter, apply, constraints are not satistfied, can't undo without canceling whole dialog

Ctrl + Backspace inserts `0x7f DEL` character instead of deleting all consecutive characters behind

Multi-select type-associated dimensions → click Instance Parameter → no effect

[Can't lock constraints of array - Autodesk Community - Revit Products](https://forums.autodesk.com/t5/revit-architecture-forum/can-t-lock-constraints-of-array/td-p/6230987)
https://forums.autodesk.com/t5/revit-api-forum/linear-dimensions-to-constraints/td-p/10753708

Need undo for sort parameters alphabetically button

No confirmation when exiting type editor (press Esc, lose your changes)
Enter and Esc behave like dialog input, except when typing in Value or Fomula, which is confusing

No max() or min() functions
https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/Creating-formula-for-the-maximum-of-three-values-in-Revit.html

# Linear Dimensions and Constraints
`Dimension.IsLocked` vs `Dimension.AreSegmentsEqual`, also `Element.CanBeLocked == True !→ Dimension.IsLocked`
Bug: 782772054, 23063803, 783072034
https://forums.autodesk.com/t5/revit-api-forum/create-linear-dimension-constraint/m-p/13084868
```python
# create a linear dimension
from Autodesk.Revit.UI.Selection import ObjectType
# be sure to pick the dimension
element_ref = uidoc.Selection.PickObject(ObjectType.Element, 'Pick the multi-segment dimension')
dimension = doc.GetElement(element_ref)
with Transaction(doc, 'Lock dimension segments') as t:
    t.Start()
    for segment in dimension.Segments:
        segment.IsLocked = True
    t.Commit()
```

```python
# this should have worked
# create linear dimension as the_dimension
refs = the_dimension.References
refids = [x.ElementId.IntegerValue for x in refs]
for x in refs:
    ref = doc.GetElement(x)
    constraints = ref.GetDependentElements(ElementCategoryFilter(BuiltInCategory.OST_Constraints))
    for x in constraints:
        c = doc.GetElement(x)
        r = c.References
        rids = [y.ElementId.IntegerValue for y in r]
        if all(y in refids for y in rids):
            with Transaction(doc, 'Set Dimension Lock') as t:
                t.Start()
                c.IsLocked = True
                t.Commit()
# I think the API does not create a Linear Dimension Style + OST_Constraints with doc.Create.NewDimension()
```
[Linear dimensions to constraints - Autodesk Community - Revit Products](https://forums.autodesk.com/t5/revit-api-forum/linear-dimensions-to-constraints/td-p/10753708)
[The Building Coder: Locked Dimensioning (typepad.com)](https://thebuildingcoder.typepad.com/blog/2009/02/locked-dimensioning.html)
[Help | Dimensions and Constraints | Autodesk](https://help.autodesk.com/view/RVT/2023/ENU/?guid=Revit_API_Revit_API_Developers_Guide_Revit_Geometric_Elements_Annotation_Elements_Dimensions_and_Constraints_html)
[Dimension.AreSegmentsEqual is always False - Autodesk Community - Revit Products](https://forums.autodesk.com/t5/revit-api-forum/dimension-aresegmentsequal-is-always-false/td-p/9497296)
https://forums.autodesk.com/t5/revit-api-forum/linear-dimensions-to-constraints/td-p/10753708
https://help.autodesk.com/view/RVT/2024/ENU/?guid=Revit_API_Revit_API_Developers_Guide_Revit_Geometric_Elements_Annotation_Elements_Dimensions_and_Constraints_html
[Re: order of References in a ReferenceArray - does it mean anything? - Autodesk Community - Revit Products](https://forums.autodesk.com/t5/revit-api-forum/order-of-references-in-a-referencearray-does-it-mean-anything/m-p/8544706/highlight/true#M36359) 
> Every click on a lock in UI (corresponding to only one segment of the dimension) creates a separate constraint.


Dimension segments have no API access [Delete DimensionSegment - Autodesk Community - Revit Products](https://forums.autodesk.com/t5/revit-api-forum/delete-dimensionsegment/td-p/8666177)

DimensionType / SpotDimensionType being used like enum in ItemFactoryBase.NewDimension()?


`BoundingBoxIntersectsFilter` returns straight FabricationPart inside or intersecting outline, but not elbows

`Outline` vs `BoundingBoxXYZ` (eg. `BoundingBoxIntersectsFilter`)
No constructor for `BoundingBoxXYZ` like `Outline`

`Curve.Evaluate(<number>, False)` generally works for `<number>` to correspond to a distance down the curve, but not if `Curve.GetParameter(0)` is not 0 and `Curve.GetParameter(0)` is not the length of the curve
[Solved: Curve.Evaluate returns unexpected result - Autodesk Community - Revit Products](https://forums.autodesk.com/t5/revit-api-forum/curve-evaluate-returns-unexpected-result/td-p/11024494)
# Documentation
`Dimension.IsLocked`: Exception: Cannot access this property if this dimension is linear shape with more than one segments.

`Curve.Evaluate`: "natural parameterization of the curve"
Maybe the same as raw curve parameter? `Curve.ComputeRawParamter`

`View.Scale` has no documentation for exceptions
> Exception: This view cannot have a scale applied.

`TextNote.Create`: "A valid point must not be father then 10 miles (approx. 16 km) from the origin."

`Document.GetProjectId()` description and remarks grammar

`ExternalCommand.Execute` "Overload this method to implement and external command within Revit."

`Autodesk.Revit.DB.FabricationPart.Create` "the index condition is not larger or equal to 0 and less than ConditionCount"
`Autodesk.Revit.DB.FabricationPart.StretchAndFit` "routing end is valid to route to."
# GUI
Moving tabs around is difficult
Reordering tabs sometimes results in tab undocking
New views open at the end, not next to the current tab
Tab coloring is necessary to keep track of open documents

#important X sometimes deletes elements without keyboard shortcut set

`Selection.SelectObjects` has no keyboard shortcut or right-click menu option to Finish

