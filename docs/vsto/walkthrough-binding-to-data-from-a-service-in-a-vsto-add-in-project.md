---
title: "Bind to data from service in VSTO add-in project"
ms.date: "02/02/2017"
ms.topic: "conceptual"
dev_langs:
  - "VB"
  - "CSharp"
helpviewer_keywords:
  - "databases [Office development in Visual Studio], scrolling records"
  - "records [Office development in Visual Studio], scrolling"
  - "data [Office development in Visual Studio], scrolling database records"
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
  - "office"
---
# Walkthrough: Bind to data from a service in a VSTO Add-in project
  You can bind data to host controls in VSTO Add-in projects. This walkthrough demonstrates how to add controls to a Microsoft Office Word document, bind the controls to data retrieved from the MSDN Content Service, and respond to events at run time.

 **Applies to:** The information in this topic applies to application-level projects for Word 2010. For more information, see [Features Available by Office Application and Project Type](../vsto/features-available-by-office-application-and-project-type.md).

 This walkthrough illustrates the following tasks:

- Adding a <xref:Microsoft.Office.Tools.Word.RichTextContentControl> control to a document at runtime.

- Binding the <xref:Microsoft.Office.Tools.Word.RichTextContentControl> control to data from a web service.

- Responding to the <xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering> event of a <xref:Microsoft.Office.Tools.Word.RichTextContentControl> control.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## Prerequisites
 You need the following components to complete this walkthrough:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] or [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

## Create a new project
 The first step is to create a Word VSTO Add-in project.

### To create a new project

1. Create a Word VSTO Add-in project with the name **MTPS Content Service**, using either Visual Basic or C#.

     For more information, see [How to: Create Office projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     Visual Studio opens the `ThisAddIn.vb` or `ThisAddIn.cs` file and adds the project to **Solution Explorer**.

## Add a web service
 For this walkthrough, use a web service called the MTPS Content Service. This web service returns information from a specified MSDN article in the form of an XML string or plain text. A later step shows how to display the returned information in a content control.

### To add the MTPS content service to the project

1. On the **Data** menu, click **Add New Data Source**.

2. In the **Data Source Configuration Wizard**, click **Service**, and then click **Next**.

3. In the **Address** field, type the following URL:

     **http://services.msdn.microsoft.com/ContentServices/ContentService.asmx**

4. Click **Go**.

5. In the **Namespace** field, type **ContentService**, and click **OK**.

6. In the **Add Reference Wizard** dialog box, click **Finish**.

## Add a content control and bind to data at runtime
 In VSTO Add-in projects, you add and bind controls at runtime. For this walkthrough, configure the content control to retrieve data from the web service when a user clicks inside the control.

### To add a content control and bind to data

1. In the `ThisAddIn` class, declare the variables for the MTPS Content Service, the content control, and the data binding.

     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#2](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#2)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#2](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#2)]

2. Add the following method to the `ThisAddIn` class. This method creates a content control at the beginning of the active document.

     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#4](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#4)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#4](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#4)]

3. Add the following method to the `ThisAddIn` class. This method initializes the objects needed to create and send a request to the web service.

     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#6](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#6)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#6](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#6)]

4. Create an event handler to retrieve the MSDN Library document about content controls when a user clicks inside of the content control and bind the data to the content control.

     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#5](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#5)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#5](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#5)]

5. Call the `AddRichTextControlAtRange` and `InitializeServiceObjects` methods from the `ThisAddIn_Startup` method. For C# programmers, add an event handler.

     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#3](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#3)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#3](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#3)]

## Test the Add-in
 When you open Word, the <xref:Microsoft.Office.Tools.Word.RichTextContentControl> control appears. The text in the control changes when you click inside it.

### To test the VSTO Add-in

1. Press **F5**.

2. Click inside of the content control.

     Information is downloaded from the MTPS Content Service and displayed inside the content control.

## See also
- [Bind data to controls in Office solutions](../vsto/binding-data-to-controls-in-office-solutions.md)
