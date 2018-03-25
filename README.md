# FirebaseChatAppLBTA
Collection, firebase, animation, TableView in code

(1) Login and Signup using same textfied in code.
    - constraints get set for hide name in login that was available in register
    - upload image and upload video using ImagePickerView
    - get image thumbnail of video 
       
        fileprivate func thumbnailImageForFileUrl(_ fileUrl: URL) -> UIImage? {
        let asset = AVAsset(url: fileUrl)
        let imageGenerator = AVAssetImageGenerator(asset: asset)
        
        do {
        
            let thumbnailCGImage = try imageGenerator.copyCGImage(at: CMTimeMake(1, 60), actualTime: nil)
            return UIImage(cgImage: thumbnailCGImage)
            
        } catch let err {
            print(err)
        }
        
        return nil
        }
    
    - perfect example of ios 9 constraints using NSAnchor of NSlayout for loginview
    - collection view of chat layout done in coding using two way
    - Uiviewcontroller have called property called inputAccesoryView
         when scrolling happens and this property will be set
          - collectionView?.keyboardDismissMode = .interactive
      
       // this inputContainerView contains TextField, Send Button, image upload button for chat APP to send message
       override var inputAccessoryView: UIView? {
        get {
            return inputContainerView
           }
        }
     
     - get height of textview of dynamic text using this func. we need to just pass String. it returns CGRect
         fileprivate func estimateFrameForText(_ text: String) -> CGRect {
          let size = CGSize(width: 200, height: 1000)
          let options = NSStringDrawingOptions.usesFontLeading.union(.usesLineFragmentOrigin)
          return NSString(string: text).boundingRect(with: size, options: options, attributes: [NSFontAttributeName: UIFont.systemFont(ofSize: 16)], context: nil)
         }
     -
    
